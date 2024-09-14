<script setup>
import { reactive, onMounted } from 'vue';
import { useRoute, RouterLink, useRouter } from 'vue-router';
import { useToast } from 'vue-toastification';
import axios from 'axios';

const route = useRoute();
const router = useRouter();
const toast = useToast();

const carId = route.params.id;

const state = reactive({
   car: {},
});

const deleteCar = async () => {
    try {

        const confirm = window.confirm('Are you sure you want to delete this car?');
        if(confirm){
            await axios.delete(`/api/cars/${carId}`);
            toast.success('Car deleted Successfully');
            router.push('/cars');
        }
    } catch (error) {
        console.error('Error deleting car ',error);
        toast.error('Car not deleted');
        
    }
}

onMounted(async () =>{
    try{
        const response = await axios.get(`/api/cars/${carId}`);
        state.car = response.data;
    }catch(error){
        console.error('Error fectching car', error);
    }
});
</script>

<template>
    car view
    <p>{{ state.car.type }}</p>
    <p>{{ state.car.description }}</p>
    <p>{{ state.car.location }}</p>
    <p>{{ state.car.price }}</p>
    <RouterLink :to="`/cars/edit/${state.car.id}`">Edit Car</RouterLink>
    <button @click="deleteCar">Delete Car</button>
</template>