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
    name:"SB",
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
        location: form.location,
        price:form.price,
        //carImage:form.carImage,
        company:{
        name:form.company.name,
        description:form.company.description
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
        form.location = state.car.location;
        form.price = state.car.price;
        //form.carImage = state.car.carImage;
        form.company.name = state.car.company.name;
        form.company.description = state.car.company.description;
    } catch (error) {
        console.error('Error fetching car ', error);
    }
});

</script>

<template>
    Edit Car
    <div class="w-4/5 m-2 bg-gray-300 place-content-center">
        <form @submit.prevent="handleSubmit" class="m-2">

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
            <option value="Camaro">Camaro</option>
        </select>
        <!--label for="carImage">Car Image</label>
        <img :src=form.carImage 
            name="carImage" 
            id="carImage"
            alt=""-->
        <label for="description">Car Description</label>
        <textarea 
            v-model="form.description"
            type="text"
            name="description" 
            id="description" 
            class="border rounded w-full py-2 px-3 mb-2" 
            required></textarea>
        <label for="location">Location</label>    
        <input 
            v-model="form.location"
            type="text"
            name="location" 
            id="location" 
            class="border rounded w-full py-2 px-3 mb-2" 
            required/>

        <label for="price">Price</label> 
        <input 
            v-model="form.price"
            type="text"
            name="price" 
            id="price" 
            class="border rounded w-full py-2 px-3 mb-2" 
            required/>    

        <label for="cname">Company Name</label> 
        <input 
            v-model="form.company.name"
            type="text"
            name="cname" 
            id="cname" 
            class="border rounded w-full py-2 px-3 mb-2" 
            required/>  

        <label for="cdescription">Company Description</label> 
        <input 
            v-model="form.company.description"
            type="text"
            name="cdescription" 
            id="cdescription" 
            class="border rounded w-full py-2 px-3 mb-2" 
            required/>  
       

            <button type="submit" class="transition ease-in-out duration-200 bg-emerald-500 
            p-2 rounded hover:bg-emerald-400 hover:shadow-inner hover:shadow-emerald-700 
            active:bg-indigo-500 active:text-white active:shadow-indigo-700 ">Update Car</button>
            
    </form>
</div>


</template>