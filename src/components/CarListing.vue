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
    <div class="transition ease-in-out duration-200 w-56 hover:shadow-xl border-transparent border-4 rounded m-2 hover:border-gray-400/25">
        <p>{{ car.type }}</p>        
        <img :src="car.carImage">
        <p>${{ car.price }}</p>
        <p>
            {{ truncatedDescription }}
        </p>
        <button @click="toggleFullDescription">
            {{ showFullDescription ? 'See Less' : 'See More' }}
        </button>
        <p>{{ car.company.name }}</p>
        <RouterLink :to="'/cars/'+car.id">Edit Car</RouterLink>
    </div>
    
</template>

<style scoped>

</style>