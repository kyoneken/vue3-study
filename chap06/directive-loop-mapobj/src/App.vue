<script setup lang="ts">
import {ref} from "vue";

const cockDataListInit = new Map<number, Cocktail>
cockDataListInit.set(2345, {id: 2345, name: "ホワイトレディ", price: 1200});
cockDataListInit.set(4412, {id: 4412, name: "ブルーハワイ", price: 1500});
cockDataListInit.set(6792, {id: 6792, name: "ニューヨーク", price: 1100});
cockDataListInit.set(8429, {id: 8429, name: "マティーニ", price: 1500});
const cocktailDataList = ref(cockDataListInit);

interface Cocktail {
  id: number;
  name: string;
  price: number;
}
</script>

<template>
  <ul>
    <li
      v-for="[id, cocktailItem] in cockDataListInit"
      v-bind:key="id">
      {{ cocktailItem.name }}の値段は{{ cocktailItem.price }}円
    </li>
  </ul>
</template>

