<script setup>
import { ref } from 'vue';


const props = defineProps({
    title: String,
    text: String,
    author: String,
})

</script>

<template>
    <div class="card">
        <h3 class="card__title">{{ title }}</h3>
        <p class="card__text">{{ text }}</p>
        <div class="card__author">{{ author }}</div>
    </div>
</template>

<style lang="scss" scoped>
    @import './styles/card.scss';
</style>