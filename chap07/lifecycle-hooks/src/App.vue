<script setup lang="ts">
import {ref, computed, onBeforeMount, onMounted, onBeforeUpdate, onUpdated, onRenderTracked, onRenderTriggered} from 'vue';
import type { DebuggerEvent } from 'vue';

const heightInit = Math.round(Math.random() * 10);
const widthInit = Math.round(Math.random() * 10);
const height = ref(heightInit);
const width = ref(widthInit);

const area = computed((): number => height.value * width.value);
const change = (): void => {
 height.value = Math.round(Math.random() * 10);
  width.value = Math.round(Math.random() * 10); 
}
onBeforeMount(() => {
  console.log(`onBeforeMount called: ${height.value} * ${width.value}`);
});
onMounted(() => {
  console.log(`onMounted called: ${height.value} * ${width.value}`);
});
onBeforeUpdate(() => {
  console.log(`onBeforeUpdate called: ${height.value} * ${width.value}`);
});
onUpdated(() => {
  console.log(`onUpdated called: ${height.value} * ${width.value}`);
});
onRenderTracked((event: DebuggerEvent) => {
  console.log(`onRenderTracked called: ${height.value} * ${width.value}`);
  console.log(event);
});
onRenderTriggered((event: DebuggerEvent) => {
  console.log(`onRenderTriggered called: ${height.value} * ${width.value}`);
  console.log(event);
});
</script>

<template>
  <p>縦が{{ height }}、横が{{ width }}の長方形の面積は{{ area }}</p>
  <button @click="change">値を変更</button>
</template>
