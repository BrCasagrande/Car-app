<script setup>
import CarListing from './CarListing.vue';
import { ref, defineProps, onMounted } from 'vue';
import { RouterLink } from 'vue-router';
import axios from 'axios';

defineProps({
    limit: Number,
    showButton: {
        type: Boolean,
        default: false
    }
});
const cars = ref([]);

onMounted(async () =>{
    try{
        const response = await axios.get('/api/cars');
        cars.value = response.data;
    }catch(error){
        console.error('Error fectching jobs', error);
    }
})
console.log(cars.value.length)
</script> 

<template>
    <section class="grid grid-cols-7 gap-4">
        <CarListing v-for="car in cars.slice(0, limit || cars.length)" :key="car.id" :car="car"/>
    </section>
    <section v-if="showButton" class="transition ease-in-out duration-300 bg-red-500 w-1/12 text-center rounded drop-shadow-lg m-4 p-1 text-white hover:bg-green-500">
        <RouterLink to="/cars">View All Cars</RouterLink>
    </section>
</template>

<style scoped>

</style>