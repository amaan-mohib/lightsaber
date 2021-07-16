<template>
  <!-- <ul class="saber-list">
        <li class="saber-content" v-for="(item,index) in sabers" :key="index">
            <Saber :name="item.name" :hilt="item.hilt"/>
        </li>
    </ul> -->

  <Landing v-if="state.gif" />

  <Carousel
    v-else
    :settings="settings"
    :breakpoints="breakpoints"
    :wrap-around="true"
    :style="{ width: 80 + '%' }"
  >
    <Slide
      class="saber-content"
      v-for="(item, index) in state.sabers"
      :key="index"
    >
      <Saber
        :name="item.name"
        :hilt="item.hilt"
        :hue="item.hue"
        :lightness="item.lightness"
        :translateY="item.translateY"
      />
    </Slide>

    <template #addons>
      <Navigation />
    </template>
  </Carousel>
</template>

<script setup>
import Saber from "./Saber.vue";
import Landing from "./Landing.vue";
import "vue3-carousel/dist/carousel.css";
import { Carousel, Slide, Navigation } from "vue3-carousel";
import { reactive } from "@vue/reactivity";
import { onMounted } from "@vue/runtime-core";

const hiltPath = "/hilts";
const sabers1 = [
  {
    name: "Green lightsaber",
    hilt: `${hiltPath}/hilt1.png`,
    hue: 120,
    lightness: "50%",
  },
];

const sabers = [
  //Green
  {
    name: "Green lightsaber",
    hilt: `${hiltPath}/hilt1.png`,
    hue: 120,
    lightness: "50%",
  },
  //Blue
  {
    name: "Blue lightsaber",
    hilt: `${hiltPath}/hilt1.png`,
    hue: 195,
    lightness: "50%",
  },
  //Yellow
  {
    name: "Yellow lightsaber",
    hilt: `${hiltPath}/hilt1.png`,
    hue: 60,
    lightness: "50%",
  },
  //Red
  {
    name: "Red lightsaber",
    hilt: `${hiltPath}/hilt1.png`,
    hue: 360,
    lightness: "50%",
  },
  //Purple
  {
    name: "Purple lightsaber",
    hilt: `${hiltPath}/hilt1.png`,
    hue: 290,
    lightness: "50%",
  },
  //Darksaber
  {
    name: "Darksaber",
    hilt: `${hiltPath}/dark-hilt.png`,
    hue: 120,
    lightness: "100%",
    translateY: "-12px",
  },
];

const settings = {
  itemsToShow: 1,
  snapAlign: "center",
};
const breakpoints = {
  700: {
    itemsToShow: 2.5,
  },
};
const state = reactive({ gif: true, sabers: sabers1 });
onMounted(() => {
  setInterval(() => {
    state.gif = false;
  }, 5000);
  setInterval(() => {
    state.sabers = sabers;
  }, 7000);
});
</script>

<style>
.saber-list {
  list-style: none;
  display: flex;
  align-items: center;
  justify-content: space-around;
  width: 100%;
}
.saber-content {
  padding: 30px;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.carousel__viewport {
  overflow-x: hidden;
  overflow-y: auto;
}
.carousel__next,
.carousel__prev {
  background-color: unset;
  font-size: 50px;
  width: auto;
  height: auto;
  color: rgb(240, 239, 239);
  transition-duration: 0.4s;
}
.carousel__next:hover,
.carousel__prev:hover {
  background: hsla(0, 0%, 19%, 0.2);
}
</style>
