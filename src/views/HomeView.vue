<script setup>
import Hero from '@/components/Hero.vue';
import HomeCards from '@/components/HomeCards.vue';
import CarsListing from '@/components/CarsListing.vue';
</script>
<template>
  <Hero />
  <HomeCards/>
  <CarsListing :limit="3" :showButton="true"/>
</template>
