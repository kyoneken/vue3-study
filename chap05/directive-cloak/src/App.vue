<script setup lang="ts">
  import {ref} from "vue";

  const hello = ref("Hello!");
</script>

<template>
  <p v-cloak>{{ hello }}</p>
</template>

<style>
[v-cloak] {
  display: none;
}
</style>