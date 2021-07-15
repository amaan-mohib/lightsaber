<template>
  <div class="gif-back" :style="{ backgroundImage: 'url(' + state.url + ')' }">
    <div v-if="state.loading" class="loader"></div>
    <img
      class="giphy"
      alt="Powered by GIPHY"
      src="/src/assets/PoweredBy_200px-White_HorizLogo.png"
    />
  </div>
</template>

<script setup>
import { reactive } from "@vue/reactivity";
import { onMounted } from "@vue/runtime-core";

const parameters = {
  api_key: "245uAZTUoY76fDHo7apB6NgQ0Mt27Llv",
  tag: "star wars",
  rating: "pg-13",
};
const api = `https://api.giphy.com/v1/gifs/random?api_key=${parameters.api_key}&tag=${parameters.tag}&rating=${parameters.rating}`;
const state = reactive({ url: "", loading: true });
async function fetchData() {
  return fetch(api, {
    method: "get",
    headers: {
      "content-type": "application/json",
    },
  })
    .then((res) => {
      return res.json();
    })
    .then((json) => {
      state.loading = false;
      state.url = json.data.image_original_url;
    });
}

onMounted(() => {
  fetchData();
});
</script>

<style>
.gif-back {
  background-color: black;
  width: 100%;
  height: 100%;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  display: flex;
  align-items: center;
  justify-content: center;
}
.loader {
  border: 10px solid #979797e5;
  border-radius: 50%;
  border-top: 10px solid #202020;
  width: 100px;
  height: 100px;
  -webkit-animation: spin 2s linear infinite; /* Safari */
  animation: spin 2s linear infinite;
}
.giphy {
  position: fixed;
  bottom: 0;
  left: 0;
}
@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
