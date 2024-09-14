<script setup>
import router from '@/router';
import { reactive, onMounted } from 'vue';
import { useRoute } from 'vue-router';
import { useToast } from 'vue-toastification';
import axios from 'axios';

const route = useRoute();

const carId = route.params.id;

const form = reactive({
    type:"Brazilia",
    description:"",
    location:"Tamashi",
    price:"",
    company:{
    name:"Shigen Box",
    description:"wakaranai"
    }
});

const state = reactive({
    car: {},
});

const toast = useToast();

const handleSubmit = async () => {
    const updateCar = {
        type:form.type,
        description:form.description,
        location:"Tamashi",
        price:"",
        company:{
        name:"Shigen Box",
        description:"wakaranai"
        }
    }
    console.log(updateCar);

    try{
        const response = await axios.put(`/api/cars/${carId}`, updateCar);
        toast.success('Car edited Successfully');
        router.push(`/cars/${response.data.id}`);
    }catch(error){
        console.error('Error fectching car', error);
        toast.error('Car not added');
    }
};


onMounted(async () => {
    try {
        const response = await axios.get(`/api/cars/${carId}`);
        state.car = response.data;

        form.type = state.car.type;
        form.description = state.car.description;
    } catch (error) {
        console.error('Error fetching car ', error);
    }
});

</script>

<template>
Add Car
<div class="w-4/5">
    <form @submit.prevent="handleSubmit">

        <select 
            v-model="form.type"
            name="type" 
            id="type" 
            class="border rounded w-full py-2 px-3 " 
            required>
        
            <option value="Suzuki">Suzuki</option>
            <option value="Yamaha">Yamaha</option>
            <option value="Toyota">Toyota</option>
            <option value="Brazilia">Brazilia</option>
            <option value="Samsung">Samsung</option>
        </select>
        
        <input 
            v-model="form.description"
            type="text"
            name="name" 
            id="name" 
            class="border rounded w-full py-2 px-3 mb-2" 
            required/>

            <button type="submit">Update Car</button>
            
    </form>
</div>


</template>