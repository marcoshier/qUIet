<template>
  <ul id="selector">
      <li class="window" @click="toggleState"></li>
      <li class="x" @click="toggleState">X</li>
  </ul>
</template>

<script>
import Window from './interface-elements/Window.vue';

export default {
    name: "Selector",
    components: {
        Window
    },
    emits:['changed-selection'],
    mounted() {
        document.querySelector(".window").classList.add("active")
    },
    methods: {
        toggleState(e) {
            let element = e.target;
            if(element.classList.contains("active")) {
                    element.classList.remove("active");
                } else {
                    element.classList.add("active");
                    this.$emit("changed-selection", element.classList[0]);
            }

            Array.from(document.querySelectorAll("li")).filter(el => el != element).forEach((el) => {
                if(el.classList.contains("active")) {
                    el.classList.remove("active");
                }
            })
        }
    }
}
</script>

<style scoped>
#selector {
    position: absolute;
    left: 0;
    top: 50%;
    transform: translateY(-50%);
    padding: 0;
    margin: 10px;
    box-sizing: content-box;
    width: 40px;
    min-height: 50px;
    border: 1px solid black;
    border-radius: 2px;
    text-align: center;
    font-size: 30px;
    font-weight: 800;
    z-index: 1000;
}

li {
    display: block;
    list-style-type: none;
    text-decoration: none;
    width: 40px;
    height: 40px;
    cursor: pointer;
}

li:hover {
    background: rgba(211, 211, 211, 0.678);
}

.active {
    background: rgba(211, 211, 211, 0.514);
}

.window {
    border-bottom: 1px solid black;
}


.window::after {
   content:"";
   border: 2px solid black;
   border-radius: 2px;
   position: relative;
   top: 6px;
   left: 6px;
   display: block;
   width: 24px;
   height: 24px;
}


</style>