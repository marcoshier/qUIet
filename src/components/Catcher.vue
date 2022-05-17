<template>
  <canvas
    ref="canvas"
    @mousemove="draw"
    @mousedown="setOrigin"
    @mouseenter="setPosition"
    @mouseup="sendDoodle"
    @resize="resize"
    id="canvas"
  ></canvas>
</template>

<script>
export default {
  name: "Catcher",
  data() {
    return {
      origin: {},
      pos: {},
      ctx: null,

      rectWidth: 0,
      rectHeight: 0,

    };
  },
  emits:['drawing-done'],
  methods: {
    resize() {
      const canvas  = this.$refs.canvas;
      const ctx = canvas.getContext("2d");
      ctx.canvas.width = window.innerWidth;
      ctx.canvas.height = window.innerHeight;
    },
    sendDoodle(e) {
      const canvas = this.$refs.canvas; 
      const ctx = canvas.getContext("2d");
      ctx.clearRect(0, 0, canvas.width, canvas.height);

      if(this.rectWidth > 30 && this.rectHeight > 30) {
        this.$emit("drawing-done", {x: this.pos.x, y: this.pos.y, width: this.rectWidth, height: this.rectHeight});
      }

    
      this.rectWidth = 0;
      this.rectHeight = 0;
    },
    setOrigin(e) {
      this.origin.x = e.clientX;
      this.origin.y = e.clientY;

      this.pos.x = e.clientX;
      this.pos.y = e.clientY;
    },
    draw(e) {
      if (e.buttons == 1) {

        const canvas = this.$refs.canvas;
        const ctx = canvas.getContext("2d");
        const pos = this.pos;

        ctx.beginPath();
        ctx.lineWidth = 4;
        ctx.lineCap = "round";
        ctx.strokeStyle = "black";
        ctx.moveTo(pos.x, pos.y);
        this.pos.x = e.clientX;
        this.pos.y = e.clientY;
        ctx.lineTo(pos.x, pos.y);
        ctx.stroke();

        this.rectWidth = Math.max(this.rectWidth, pos.x - this.origin.x);
        this.rectHeight = Math.max(this.rectHeight, pos.y - this.origin.y)

      }
    }
  },

  mounted() {
    this.resize()
  }
};
</script>

<style>
canvas {
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  z-index: 999;
  background: transparent;
}
</style>
