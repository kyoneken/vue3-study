<script setup lang="ts">
import { reactive, provide } from 'vue';
import BaseSection from './components/BaseSection.vue';
import type { Member } from '@/interfaces';

// 会員情報リストの作成
const memberList = new Map<number, Member>();
memberList.set(1, { id: 1, name: '山田太郎', email: 'yamada@test.com', points: 100, note: '特別会員' });
memberList.set(2, { id: 2, name: '田中花子', email: 'tanaka@test.com', points: 200});

// 会員情報リストのProvide
provide("memberList", reactive(memberList));
</script>

<template>
<BaseSection />
</template>
