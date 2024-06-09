<script setup lang="ts">
import {ref} from "vue";

const widthOrHeght = ref("height");
const widthOrHeghtValue = ref(500);

</script>

<template>
  <p><img alt="VueLogo" src="./assets/logo.svg" v-bind:[widthOrHeght]="widthOrHeghtValue"></p>
</template>
