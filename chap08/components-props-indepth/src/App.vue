<script setup lang="ts">
import { ref, computed } from 'vue'
import OneMember from './components/OneMember.vue';

interface Member {
    id: number;
    name: string;
    email: string;
    points: number;
    note?: string;
}

// 会員リストデータを用意
const memberListInit = new Map<number, Member>();
memberListInit.set(33456, {
    id: 33456,
    name: '山田太郎',
    email: 'yamada@test.com',
    points: 100,
    note: '初回入会特典あり'
});
memberListInit.set(47783, {
    id: 47783,
    name: '佐藤花子',
    email: 'sato@test.com',
    points: 200
});

const memberList = ref(memberListInit);

// 会員リストのポイント合計を算出
const totalPoints = computed(
    (): number => {
      let total = 0;
      for(const member of memberList.value.values()) {
        total += member.points;
      }
      return total;
    }
)
</script>

<template>]
  <section>
    <h1>会員リスト</h1>
    <p>全会員の保有ポイント合計: {{ totalPoints }}</p>
    <OneMember v-for="[id, member] in memberList"
                v-bind:key="id"
                v-bind:id="id"
                v-bind:name="member.name"
                v-bind:email="member.email"
                v-bind:points="member.points"
                v-bind:note="member.note" />
  </section>
</template>

