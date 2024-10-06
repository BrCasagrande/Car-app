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
    <section class="grid  md:grid-cols-7 gap-4 place-content-center">
        <CarListing v-for="car in cars.slice(0, limit || cars.length)" :key="car.id" :car="car"/>
    </section>
    <section v-if="showButton">
        <RouterLink to="/cars" class="transition ease-in-out duration-300 bg-red-500 w-1/12 text-center rounded drop-shadow-lg m-2 p-2 text-white hover:bg-green-500">View All Cars</RouterLink>
    </section>
</template>

<style scoped>

</style>