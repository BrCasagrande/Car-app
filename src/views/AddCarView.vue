<script setup>
import router from '@/router';
import { reactive, ref } from 'vue';
import { useToast } from 'vue-toastification';
import axios from 'axios';

const form = reactive({
    type:"Brazilia",
    description:"",
    location:"Tamashi",
    price:"",
    //carImage:"",
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
        price:form.price,
        carImage:"fiat-logo-2.png",
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

const onChangeFile = (event)=> {
      this.$emit('update:modelValue', event.target.files[0])
    }

</script>

<template>
<div class="w-4/5 p-2 md:p-12">
    <h2 class="font-bold p-2 ">New Car</h2>
    <form @submit.prevent="handleSubmit">
        <label for="car">Brand</label>
        <section class="m-2">
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
        </section>
        <label for="price">Price</label>
        <section class="m-2">
            <input  v-model="form.price"
                name="price" 
                type="number"
                id="price" 
                class="border rounded w-full py-2 px-3 " 
                required/>
        </section>
        <!--input type="file" @change="onChangeFile" name="file" />
        <MyInputFileComponent v-model="form.carImage" /-->
        <label for="car">Description</label>
        <section class="m-2">
            <textarea
                v-model="form.description"
                type="text"
                name="name" 
                id="name" 
                class="border rounded w-full py-2 px-3 mb-2" 
                required>
            </textarea>

        </section>

        
            <button type="submit" class=" hover:bg-gradient-to-b from-green-400 to-emerald-600 p-2 border rounded bg-gray-500">Add Car</button>            
    </form>

   
</div>


</template>
