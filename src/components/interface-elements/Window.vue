<template>
  <div ref="window" id="window">
      <p>TITLE</p>
  </div>
</template>

<script>
export default {
    name: "Window",
    props: {
      currentElement: {
        pos: {
            x: Number,
            y: Number
        },
        size: {
          width: Number,
          height: Number
        },
        index: Number
      }
    },
    mounted() {
        let el = this.$refs.window

        el.style.left = this.currentElement.pos.x + "px";
        el.style.top = this.currentElement.pos.y + "px";  
        
        el.style.width = this.currentElement.size.width + "px";
        el.style.height = this.currentElement.size.height + "px";
    }
}
</script>

<style scoped>
    #window {
        position: absolute;
        top: 0;
        left: 0;
        padding: 0;
        width: 0;
        height: 0;
        border: 3px solid #f9ffb7;
        border-radius: 4px;
        background: grey;
        z-index: 5;
        overflow: hidden;
    }

    #window::after {
      content:"TITLE";
      font-family: monospace;
      text-align: left !important;
      font-size: 13px;
      text-transform: uppercase;
      position: absolute;
      color: #f9ffb7;
      width: 100%;
      top: 2px;
      left: 4px;
    }

    p {
        position: absolute;
        font-family: monospace;
        margin: 0;
        width: 0;
        height: 0;
        overflow: hidden;
        top: 0;
        left: 4px;
        display: block;
        text-align: left;
    }

</style>