<script setup lang="ts">
import OneInfo from './components/OneInfo.vue';
import {ref} from 'vue';

const propsTitle = ref("発生した乱数");
const rand = Math.round(Math.random() * 100);
const propContent = ref(rand);
</script>

<template>
  <h1>基礎</h1>
  <section>
    <h2>テンプレート変数を利用。</h2>
    <OneInfo
      v-bind:title="propsTitle"
      v-bind:content="propContent"
      />
  </section>

</template>

<style>
section {
  border: blue 1px solid;
  margin: 10px;
}
</style>