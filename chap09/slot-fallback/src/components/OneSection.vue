<script setup lang="ts">
interface Props {
    name: string
}
defineProps<Props>();
</script>

<template>
    <section class="box">
        <h1>{{ name }}さんの状況</h1>
        <slot>
            <p>情報がありません。</p>
        </slot>
    </section>
</template>
<style>
.box {
    border: greenq 1px solid;
    margin: auto;
}
</style>