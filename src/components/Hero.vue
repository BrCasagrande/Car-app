<script setup>
import { defineProps } from 'vue';
defineProps({
    title:{
        type: String,
        default:'Became a Dev'
    },
    subtitle:{
        type: String,
        default:'Became a Front-end'
    }
})
</script>

<template>
    <h3>
        {{title}}
    </h3>
    <p>{{ subtitle }}</p>
    <img src="../img/banner.jpg" alt="">
</template>