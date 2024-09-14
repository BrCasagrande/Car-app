<script setup>
import { onMounted, ref } from "vue";

    const name = 'Bruno Casagrande';
    const status = ref('ativo');
    const tasks = ref(['Task1','Task2','Task3']);
    const newTask = ref('');
    
    const toggleStatus = () =>{
      if (status.value === 'ativo') {
      status.value = 'inativo'
      }
      else{
        status.value='ativo'
      }
    };

    const addTask = () =>{
      if(newTask.value.trim()!==''){
        tasks.value.push(newTask.value);
        newTask.value='';
      }
    }
    const deleteTask =(index) =>{
      tasks.value.splice(index,1);
    };

    onMounted(async () =>{
      try{
        const response = await fetch('https://jsonplaceholder.typicode.com/todos');
        const data = await response.json();
        tasks.value = data.map((task) => task.title)
      }catch(error){
        console.log('Error fetching tasks');
      }
    });
 
</script>

<template>
  <h1>Oi {{ name }}</h1>

  <p></p>
  <p v-if="status === 'ativo'">Usuario ativo</p>
  <p v-else>Usuario inativo</p>

  <form @submit.prevent="addTask">
    <label for="new Task">Add Task</label>
    <input type="text" id="newTask" name="newTask" v-model="newTask">
    <button type="submit">Submit</button>
  </form>

  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>
        {{ task }}
      </span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>
  <a :href="link" target="_blank">Saiba mais</a>
  <button @click="toggleStatus">Change status</button>
</template>

<style scoped>

</style>
