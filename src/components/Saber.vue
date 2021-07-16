<template>
  <div class="flex container carousel__item">
    <div class="flex">
      <div class="blade"></div>
      <img class="hilt" :src="hilt" />
      <!-- <div class="hilt" :style="{ backgroundImage: 'url(' + hilt + ')' }"></div> -->
    </div>
    <h1 class="title">{{ name }}</h1>
  </div>
</template>

<script setup>
import { reactive } from "@vue/reactivity";
import { onMounted } from "@vue/runtime-core";

const props = defineProps({
  name: String,
  hilt: String,
  hue: Number,
  lightness: String,
  translateY: Number,
});
const state = reactive({
  hue: props.hue,
  lightness: props.lightness,
  translateY: props.translateY,
  scale: 0,
  background: "white",
  radius: "500px 500px 0 0",
});
onMounted(() => {
  state.background = props.lightness === "100%" ? "black" : "white";
  state.radius =
    props.lightness === "100%" ? "100% / 500px 20px 0 0" : "500px 500px 0 0";
  state.translateY = state.translateY || "0px";
  setTimeout(() => {
    state.scale = 1;
  }, 500);
});
</script>

<style scoped>
.flex {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.blade {
  position: relative;
  background: v-bind("state.background");
  height: 57vh;
  max-height: 432px;
  width: 80%;
  max-width: calc(0.8 * 20px);
  border-radius: v-bind("state.radius");
  box-shadow: inset 0 0 4px
      hsl(v-bind("state.hue") 100% v-bind("state.lightness") / 1),
    0 0 1em hsl(v-bind("state.hue") 100% v-bind("state.lightness") / 0.8),
    0 0 1.5em hsl(v-bind("state.hue") 100% v-bind("state.lightness") / 0.7),
    0 0 2em hsl(v-bind("state.hue") 100% v-bind("state.lightness") / 0.5),
    0 0 3em hsl(v-bind("state.hue") 100% v-bind("state.lightness") / 0.3),
    0 0 5em hsl(v-bind("state.hue") 100% v-bind("state.lightness") / 0.2);
  transition: transform 50ms ease-out;
  transform-origin: bottom;
  transform: scaleY(v-bind("state.scale"));
}
.blade::after {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: hsl(v-bind("state.hue") 100% v-bind("state.lightness"));
  border-radius: inherit;
  filter: blur(0.5rem);
  opacity: 1;
  animation: pulse linear 5s infinite;
}
.blade::before {
  content: "";
  position: absolute;
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  background: v-bind("state.background");
  border-radius: inherit;
  z-index: 10;
}
.hilt {
  height: calc(7rem - v-bind("state.translateY"));
  min-width: 20px;
  user-select: none;
  transform: translateY(v-bind("state.translateY"));
  /* background-size: contain;
  background-repeat: no-repeat;
  background-position: top; */
}
@keyframes pulse {
  50% {
    opacity: 0.5;
  }
}
.container {
  width: 100%;
}
.container .title {
  margin-top: 20px;
}
@media (hover) {
  .container .title {
    display: none;
    margin-top: 20px;
  }
  .container:hover {
    background: hsla(0, 0%, 19%, 0.2);
    backdrop-filter: blur(10px);
    width: 100%;
    padding: 30px;
    cursor: pointer;
    /* transform: scale(1.1); */
    transition-duration: 0.4s;
    border-radius: 10px;
    box-shadow: 0 0 5px 2px hsl(0, 0%, 80%);
  }
  .container:hover .title {
    display: block;
  }
}
</style>