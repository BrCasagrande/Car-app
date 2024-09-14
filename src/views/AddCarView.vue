<script setup>
import router from '@/router';
import { reactive } from 'vue';
import { useToast } from 'vue-toastification';
import axios from 'axios';

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

const toast = useToast();

const handleSubmit = async () => {
    const newCar = {
        type:form.type,
        description:form.description,
        location:"Tamashi",
        price:"",
        company:{
        name:"Shigen Box",
        description:"wakaranai"
        }
    }
    console.log(newCar);

    try{
        const response = await axios.post('/api/cars/', newCar);
        toast.success('Car add Successfully');
        router.push(`/cars/${response.data.id}`);
    }catch(error){
        console.error('Error fectching car', error);
        toast.error('Car not added');
    }
};

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

            <button type="submit">Add Car</button>
            
    </form>
</div>


</template>