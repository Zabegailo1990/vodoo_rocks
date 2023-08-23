<script setup>
import { ref } from 'vue';
import Icon from '../Icon/index.vue';

const props = defineProps({
    modelValue: String,
    placeholder: String,
})

const inputActive = ref(false)

const emit = defineEmits(['update:modelValue']);
const onInput = (event) => {
    emit('update:modelValue', event.target.value);
};

</script>

<template>
    <div class="search">
        <div class="search__icon">
            <Icon name="search" />
        </div>
        <input 
            type="text" 
            class="search__input"
            :class="{ 'search__input--active': inputActive }"
            :value="modelValue"
            :placeholder="placeholder"
            @focus="inputActive = true"
            @blur="inputActive = false"
            @input="onInput"
        />
    </div>
</template>

<style lang="scss" scoped>
    @import './styles/search.scss';
</style>