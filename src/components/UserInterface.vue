<template>
  <div ref="windows">
    <Window v-for="(el, index) in elements" v-bind:currentElement="el" :key="index"/>
  </div>
  <Selector @changed-selection='changedSelection'/>
</template>

<script>
import Selector from './Selector.vue';

import Window from './interface-elements/Window.vue';

export default {
    components: {
        Selector,
        Window
    },
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
    data() {
      return {
        isX: false, 
        elements: [],
      }
    },
    methods: {
      changedSelection(sel) {
        if(sel == "window") {
            this.isX = false
        } else {
            this.isX = true
        }
      }
    },
    watch: {
        currentElement: {
          handler(newVal, oldVal) {
            if(newVal != oldVal) {


              if(this.isX == false) {
                this.elements.push(newVal)
              } else {
                Array.from(this.$refs.windows.children).forEach((w) => {
                  // get center of the x
                  let posX = this.currentElement.pos.x + (this.currentElement.size.width / 2)
                  let posY = this.currentElement.pos.y + (this.currentElement.size.height / 2)


                  let rect = w.getBoundingClientRect()

                  console.log(rect)

                  if(posX > rect.x && posY > rect.y && posX < (rect.x + rect.width) && posY < (rect.y + rect.height)) {
                     //console.log("it is inside");
                     w.remove()
                   } else {
                     //console.log("posX ", posX, " > rect.x ", rect.x, ", posY ", posY, " > rect.y ", rect.y, ", posX ", posX, " < (rect.x + rect.width) ", rect.x + rect.width, ", posY ", posY, ", rect.y + rect.height ", rect.y + rect.height,);
                   }

                })
              }
            }
          }
        }
    }
}
</script>

<style>

</style>