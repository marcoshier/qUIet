<template>
  <header>
    <h1>qUIet!</h1>
  </header>
  <Catcher @drawing-done='nextElement'/>
  <UserInterface :currentElement="currentElement"/>
</template>

<script>
import Catcher from './components/Catcher.vue';
import UserInterface from './components/UserInterface.vue';

export default {
  name: "App",
  components: { Catcher, UserInterface },
  data() {
    return {
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
    }
  },
  mounted() {
    this.currentElement.index = -1
  },
  methods: {
    nextElement(data) {
      
      if(this.currentElement.index == 3) {
       this.currentElement.index = -1 
      }
      let index = this.currentElement.index + 1

      this.currentElement = {
        pos: {
          x: data.x,
          y: data.y
        },
        size: {
          width: data.width,
          height: data.height
        },
        index: index
      }

    }
  }
};
</script>


<style>
h1 {
  font-family: 'Courier New', Courier, monospace;
  position: absolute;
  top: 0;
  left: 10px;
  font-size: 18px;
  color: black
}

body, html {
  margin: 0;
  padding: 0;
  overflow: hidden;
}

body {
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  z-index: 2;
  background: transparent;
}

#app {
  width: 100vw;
  height: 100vh;
  margin: 0;
  padding: 0;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  background: grey;
  /* background: radial-gradient(circle, rgba(230,255,176,1) 0%, rgba(255,255,255,1) 96%); */
}
</style>
