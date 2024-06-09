<script setup lang="ts">
import {ref, computed} from "vue";

const radiusInt = Math.round(Math.random() * 10);
const PI = ref(3.14);
const radius = ref(radiusInt);

// 円面積の算出プロパティを用意
const area = computed((): number => {
  return radius.value * radius.value * PI.value;
});

// 半径のテンプレート変数に新しい乱数を1秒ごとに格納
setInterval((): void => {
  radius.value = Math.round(Math.random() * 10);
}, 1000);
</script>

<template>
  <p>半径{{ radius }}の円の面積を円周率{{ PI }}で計算すると、{{ area }}</p>
</template>

