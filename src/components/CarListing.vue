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
const deleteItemById = (id)=> {
      // Filter out the item with the matching ID
      this.items = this.items.filter(item => item.id !== id);
    }

</script>

<template>
    <div class="transition ease-in-out duration-500 w-56 drop-shadow-xl shadow-blue-500 rounded m-2 border hover:scale-125 hover:bg-amber-100" >
        <p class="p-1">{{ car.type }}</p>        
        <img class="rounded" :src="car.carImage">
        <p class="p-1">${{ car.price }}</p>
        <p class="p-1">
            {{ truncatedDescription }}
        </p>
        <button class="p-1" @click="toggleFullDescription">
            {{ showFullDescription ? 'See Less' : 'See More' }}
        </button>
        <p class="p-1">{{ car.company.name }}</p>
        <RouterLink :to="'/cars/edit/'+car.id" >
            <svg  xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-8 p-1 m-2 bg-indigo-400 rounded">
                <path stroke-linecap="round" stroke-linejoin="round" d="m16.862 4.487 1.687-1.688a1.875 1.875 0 1 1 2.652 2.652L10.582 16.07a4.5 4.5 0 0 1-1.897 1.13L6 18l.8-2.685a4.5 4.5 0 0 1 1.13-1.897l8.932-8.931Zm0 0L19.5 7.125M18 14v4.75A2.25 2.25 0 0 1 15.75 21H5.25A2.25 2.25 0 0 1 3 18.75V8.25A2.25 2.25 0 0 1 5.25 6H10" />
            </svg>
        </RouterLink>
        <div @click="deleteItemById(car.id)">{{car.id}}</div>
    </div>
    
</template>

<style scoped>

</style>