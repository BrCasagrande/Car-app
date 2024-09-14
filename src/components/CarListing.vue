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
    <div>
        <p>{{ car.type }}</p>
        <p>{{ car.price }}</p>
        <p>
            {{ truncatedDescription }}
        </p>
        <button @click="toggleFullDescription">
            {{ showFullDescription ? 'Less' : 'More' }}
        </button>
        <p>{{ car.company.name }}</p>
        <RouterLink :to="'/cars/'+car.id">#</RouterLink>
    </div>
    
</template>

<style scoped>

</style>