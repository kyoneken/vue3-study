<script setup lang="ts">
import {ref, watchEffect} from "vue";

const cocktailNo = ref(1);
const priceMsg = ref("");

watchEffect(
  (): void => {
    priceMsg.value = getCocktailInfo(cocktailNo.value);
  }
);

setInterval(
  (): void => {
    cocktailNo.value = Math.round(Math.random() * 3) + 1;
  },1000
);

interface Cocktail {
  id: number;
  name: string;
  price: number;
}

function getCocktailInfo(cocktailNo: number): string {
  const cockDataListInit = new Map<number, Cocktail>();
  cockDataListInit.set(1, {id: 1, name: "ホワイトレディ", price: 1200});
  cockDataListInit.set(2, {id: 2, name: "ブルーハワイ", price: 1500});
  cockDataListInit.set(3, {id: 3, name: "ニューヨーク", price: 1100});
  cockDataListInit.set(4, {id: 4, name: "マティーニ", price: 1500});

  const cocktail = cockDataListInit.get(cocktailNo);
  let msg = "該当カクテルはありません";
  if(cocktail != undefined) {
    msg = `該当のカクテルは${cocktail.name}で、価格は${cocktail.price}円です。`;
  }

  return msg;
}

</script>

<template>
  <p>現在のカクテル番号：{{ cocktailNo }}</p>
  <p>{{ priceMsg }}</p>
</template>
