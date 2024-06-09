<script setup lang="ts">
import {ref} from "vue";

// 現在日時を取得。
const now = new Date();
const nowStr = now.toLocaleTimeString();
// 現在の時刻文字列をテンプレート変数として用意
let timeStr = nowStr;
// 同じく現在の時刻文字列をテンプレート変数としてref()で用意
const timeStrRef = ref(nowStr);

// 新しい時刻に変換
function changeTime(): void {
  //現在日時を取得
  const newTime = new Date();
  const newTimeStr = newTime.toLocaleTimeString();
  timeStr = newTimeStr;
  timeStrRef.value = newTimeStr;
}
// changeTime関数を1秒ごとに実行
setInterval(changeTime, 1000);
</script>

<template>
  <p>現在時刻：{{timeStr}}</p>
  <p>現在時刻(ref)：{{timeStrRef}}</p>
</template>

