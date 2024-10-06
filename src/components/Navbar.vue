<script setup>
import { RouterLink } from 'vue-router';

const navStyle = "transition ease-in-out duration-300 content-center h-full hover:bg-gradient-to-b from-gray-500 to-gray-700 hover:text-zinc-300 p-1";
</script>

<template>
    <nav class="font-bold space-x-2 bg-gradient-to-b from-slate-400 to-slate-600 h-12 flex">
        <RouterLink to="/" ><img src="../img/fiat-logo-2.png" alt="Fiat" class="h-full"></RouterLink>
        <RouterLink to="/" :class=navStyle>Home</RouterLink>
        <RouterLink to="/cars" :class=navStyle>Cars</RouterLink>
        <RouterLink to="/cars/add" :class=navStyle>Add Car</RouterLink>
        <RouterLink to="/about" :class=navStyle>About Us</RouterLink>
       
    </nav>
</template>