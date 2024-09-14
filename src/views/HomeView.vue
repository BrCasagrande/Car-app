<script setup>
import Hero from '@/components/Hero.vue';
import HomeCards from '@/components/HomeCards.vue';
import CarsListing from '@/components/CarsListing.vue';
</script>
<template>
  <Hero title="Want to buy?" subtitle="Want to Sell?"/>
  <HomeCards/>
  <CarsListing :limit="3" :showButton="true"/>
</template>
