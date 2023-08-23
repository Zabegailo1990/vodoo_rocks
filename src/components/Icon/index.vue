<script setup>
import sprite from './sprite/icons-sprite.svg';

const props = defineProps({
    name: String,
    color: String,
});

</script>

<template>
    <svg class="icon">
        <use :xlink:href="`${sprite}#icon-${props.name}`" />
    </svg>
</template>

<style lang="scss" scoped>
    @import './styles/icon.scss';
</style>