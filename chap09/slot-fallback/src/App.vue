<script setup lang="ts">
import { ref } from 'vue';
import OneSection from './components/OneSection.vue';

const taro = ref('Taro Tanaka');
const hanako = ref('Hanako Yamada');
</script>

<template>
<section>
  <h2>Slotの利用</h2>
  <OneSection v-bind:name="taro">
    <p>連絡がつきません。</p>
  </OneSection>
  <OneSection v-bind:name="hanako" />
</section>
</template>