<script setup>

import HomeCards from '@/components/HomeCards.vue';
import CarsListing from '@/components/CarsListing.vue';
</script>
<template>
    <CarsListing :limit="3" :showButton="true"  />
</template>
