<template>
  <img :src="image" />
</template>

<script setup lang="ts">
import { onMounted, onUnmounted, ref } from "vue";
import getImages from "./helper/getImages";

const images = ref([])
const image = ref();

function getRandom() {
  const random = Math.floor(Math.random() * images.value.length);
  return images.value[random];
}

let interval: number;

onMounted(() => {
  getImages().then((data: any[]) => images.value = data);

  interval = setInterval(() => {
    image.value = getRandom();

  }, 3000);
  console.log(interval);
});

onUnmounted(() => clearInterval(interval));

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
