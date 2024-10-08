<script setup>
import Navbar from './components/Navbar.vue';
import { RouterView } from 'vue-router';
import Hero from '@/components/Hero.vue';

</script>
<template>
  <Hero title="Want to buy?" subtitle="Want to Sell?"/>
  <Navbar/>
  <RouterView />
</template>