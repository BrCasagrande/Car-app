<script setup>
import Card from './Card.vue';
import { RouterLink } from 'vue-router';
</script>

<template>
    <div>
        <Card>1</Card>
    </div>
    <div>
        <Card bg="bg-red-100">2</Card>
    </div>
</template>

<style scoped>
div{
    height: 100px;
    width: 20%;    
}
</style>