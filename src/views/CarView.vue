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
    <h2>Car View</h2>
    <section class="grid justify-items-center">
        <div class="grid grid-cols-2 p-2 rounded auto-cols-min w-9/12 bg-slate-200 text-justify ">
            <section >
                <p>{{ state.car.type }}</p>
                <img  :src="'/src/img/'+ state.car.carImage ">
            </section>

            <section class="p-4" >
                <div class="h-5/6">
                    <h4>Description</h4>
                    <p class="my-2">{{ state.car.description }}</p>
                    <p>Location:{{ state.car.location }}</p>
                    <p>Price: ￥ {{ state.car.price }}</p>
                </div>
                <div class="grid grid-cols-2 text-center items-end">
                    <RouterLink :to="`/cars/edit/${state.car.id}`" class="bg-emerald-300 rounded p-2 m-4 hover:bg-emerald-500">Edit Car</RouterLink>
                    <button @click="deleteCar" class="bg-red-300 rounded p-2 m-4 hover:bg-red-500">Delete Car</button>
                </div>
            </section>
        </div>

    </section>
</template>