<template>
    <div v-if="props.content">
        <h1>{{ props.content.title }}</h1>
        <p>{{ props.content.content }}</p>
        <button v-for="(response, index) in props.content.response" :key="index">{{ response }}</button>
    </div>
</template>

<script setup lang="ts">
import type { TContentStory } from '@/types/global';

const props = defineProps<{
    content: TContentStory | null
}>();
</script>

<style lang="scss" scoped>
    
</style>