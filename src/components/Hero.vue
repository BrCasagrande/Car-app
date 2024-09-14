<script setup>
import { defineProps } from 'vue';
import { RouterLink } from 'vue-router';
defineProps({
    title:{
        type: String,
        default:'Volkswagen das Auto'
    },
    subtitle:{
        type: String,
        default:'Fiat'
    }
})
</script>

<template>
    <h3 class="bg-gradient-to-b from-green-700 to-emerald-800 p-2 font-bold text-gray-300 content-center flex justify-center">
       <span class="animate-pulse">
        <RouterLink to="/cars"> {{ title }}</RouterLink>           
       </span> 
    </h3 >
    <p class="bg-gradient-to-b from-red-700 to-orange-800 p-2 font-bold text-gray-300 content-center flex justify-center">
      <span>
        <RouterLink to="/cars/add" > {{ subtitle }}</RouterLink> 
      </span>  
    </p>
    <img class="w-full " src="../img/banner.png" alt="" >
</template>