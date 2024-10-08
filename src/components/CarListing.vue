<script setup>
import { defineProps, ref, computed } from 'vue';
import { RouterLink } from 'vue-router';


const props = defineProps({
    car: Object,
})

const showFullDescription = ref(false);
const toggleFullDescription = () =>{
    showFullDescription.value = !showFullDescription.value;
} ;

const truncatedDescription = computed(() => {
    let description = props.car.description;

    if(!showFullDescription.value){
        description = description.substring(0,3)+"...";
    }
    return description;
}) 


</script>

<template>
    <div class="transition ease-in-out duration-500 w-56 drop-shadow-xl hover:shadow rounded m-2 border hover:scale-105 " >
        <p class="p-1 bg-gradient-to-b from-gray-200 to-gray-400 font-bold">{{ car.type }}</p>        
        <img :src="'/src/img/'+car.carImage">
        <p class="p-1">${{ car.price }}</p>
        <p class="p-1">
            {{ truncatedDescription }}
        </p>
        <button class="p-1 flex" @click="toggleFullDescription">
            {{ showFullDescription ? 'See Less' : 'See More' }}
            <svg v-if="showFullDescription" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                <path stroke-linecap="round" stroke-linejoin="round" d="m4.5 15.75 7.5-7.5 7.5 7.5" />
            </svg>
            <svg v-else xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
                <path stroke-linecap="round" stroke-linejoin="round" d="m19.5 8.25-7.5 7.5-7.5-7.5" />
            </svg>
        </button>



        <p class="p-1">{{ car.company.name }}</p>
        <RouterLink :to="'/cars/'+car.id" class="transition ease-in-out duration-200 flex size-8 p-1 m-2 hover:bg-indigo-400 border rounded">
            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" >
                <path stroke-linecap="round" stroke-linejoin="round" d="M9 12h3.75M9 15h3.75M9 18h3.75m3 .75H18a2.25 2.25 0 0 0 2.25-2.25V6.108c0-1.135-.845-2.098-1.976-2.192a48.424 48.424 0 0 0-1.123-.08m-5.801 0c-.065.21-.1.433-.1.664 0 .414.336.75.75.75h4.5a.75.75 0 0 0 .75-.75 2.25 2.25 0 0 0-.1-.664m-5.8 0A2.251 2.251 0 0 1 13.5 2.25H15c1.012 0 1.867.668 2.15 1.586m-5.8 0c-.376.023-.75.05-1.124.08C9.095 4.01 8.25 4.973 8.25 6.108V8.25m0 0H4.875c-.621 0-1.125.504-1.125 1.125v11.25c0 .621.504 1.125 1.125 1.125h9.75c.621 0 1.125-.504 1.125-1.125V9.375c0-.621-.504-1.125-1.125-1.125H8.25ZM6.75 12h.008v.008H6.75V12Zm0 3h.008v.008H6.75V15Zm0 3h.008v.008H6.75V18Z" />
            </svg>

           

        </RouterLink>
    </div>
    
</template>

<style scoped>

</style>