<script setup lang="ts">
  import {computed} from "vue";

  const randomNumber = computed(
    (): number => {
      return Math.round(Math.random() * 100);
    }
  );
</script>

<template>
  <p>
    点数は{{randomNumber}}点で
    <span v-if="randomNumber >= 80">優</span>
    <span v-else-if="randomNumber >= 70">良</span>
    <span v-else-if="randomNumber >= 60">可</span>
    <span v-else>不可</span>
  </p>
</template>

