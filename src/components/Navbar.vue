<script setup>
import { RouterLink } from 'vue-router';

</script>

<template>
    <nav class="space-x-2">
        <RouterLink to="/">home</RouterLink>
        <RouterLink to="/cars">cars</RouterLink>
        <RouterLink to="/cars/add">Add</RouterLink>
        <RouterLink to="/about">voce</RouterLink>
    </nav>
</template>