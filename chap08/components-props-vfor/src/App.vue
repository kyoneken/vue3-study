<script setup lang="ts">
import {ref} from "vue";
import OneInfo from "./components/OneInfo.vue";

const weatherListInit = new Map<number, Weather>();
weatherListInit.set(1, {id: 1, title: "今日の天気", content: "It's sunny today."});
weatherListInit.set(2, {id: 2, title: "明日の天気", content: "It will be rainy tomorrow."});
weatherListInit.set(3, {id: 3, title: "明後日の天気", content: "It will be cloudy the day after tomorrow."});
const weatherList = ref(weatherListInit);

interface Weather {
  id: number;
  title: string;
  content: string;
}
</script>

<template>
  <h1>基礎</h1>
  <section>
    <OneInfo
      v-for="[id, weather] in weatherList"
      v-bind:key="id"
      v-bind:title="weather.title"
      v-bind:content="weather.content" />
  </section>
</template>

