<script setup lang="ts">
import { computed, inject } from "vue";
import OneMember from './OneMember.vue';
import type { Member } from '@/interfaces';

// 会員情報リストのInject
const memberList = inject("memberList") as Map<number, Member>;
// 保有ポイントの合計値の算出
const totalPoints = computed(
    (): number => {
        let total = 0;
        memberList.forEach((member) => {
            total += member.points;
        });
        return total;
    }
);
</script>

<template>
    <section class="box">
        <h1>会員情報一覧</h1>
        <p>合計ポイント: {{ totalPoints }}</p>
        <OneMember 
            v-for="id in memberList.keys()" 
            v-bind:key="id" 
            v-bind:id="id" />
    </section>
</template>

<style scoped>
section {
    border: 1px dashed orange;
    margin: 10px;
}
</style>