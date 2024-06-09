<script setup lang="ts">
import {ref, computed} from "vue";

const msg = ref("Hello world");
const msgTextRed = ref("red");
const msgTextColor = ref("white");
const msgBgColor = ref("black");
const msgStyles = ref({
  color: "white",
  backgroundcolor: "black"
});
const msgStyle2 = ref({
  fontSize: "24pt"
});
const msgStyle3 = ref({
  color: "pink",
  fontSize: "24pt"
});
const textSize = computed(
  (): string => {
    const size = Math.round(Math.random() * 25) + 10;
    return `${size}pt`;
  }
);
</script>

<template>
  <p v-bind:style="{color: msgTextRed}">
    {{ msg }}
  </p>
  <p v-bind:style="{color: 'pink'}">
    {{ msg }}
  </p>
  <p v-bind:style="{fontSize: textSize}">
    {{ msg }}
  </p>
  <p v-bind:style="{color: msgTextColor, backgroundColor: msgBgColor}">
    {{ msg }}
  </p>
  <p v-bind:style="{color: msgTextColor, 'background-color': msgBgColor}">
    {{ msg }}
  </p>
  <p v-bind:style="msgStyles">
    {{ msg }}
  </p>
  <p v-bind:style="[msgStyles, msgStyle2]">
    {{ msg }}
  </p>
  <p v-bind:style="[msgStyles, msgStyle3]">
    {{ msg }}
  </p>
  <p v-bind:style="[msgStyle3, msgStyles]">
    {{ msg }}
  </p>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
