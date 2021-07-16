<template>
  <SabersList />
</template>

<script setup>
import SabersList from "./components/SabersList.vue";
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Saira:wght@100;300;400;500;600;700&display=swap");
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  /* background-color: #01011a; */
  font-family: "Saira", sans-serif;
  background-color: #130f40;
  background-image: linear-gradient(315deg, #130f40 0%, #000000 74%);
  background-size: cover;
  color: rgb(240, 239, 239);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  font-family: "Saira", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  height: 100vh;
  display: flex;
  width: 100%;
  align-items: center;
  justify-content: space-around;
}
</style>
