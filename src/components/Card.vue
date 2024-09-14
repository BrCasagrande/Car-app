<script setup>
import { defineProps } from 'vue';
defineProps({
    bg:{
        type: String,
        default: 'bg-gray-100'
    }
})
</script>

<template>
    <div :class="`${bg}`">
        <slot></slot>
    </div>
</template>

<style scoped>
div{
    height: 200px;
    width: 20%;
    padding: 5%;
}
</style>