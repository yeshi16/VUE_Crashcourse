<script setup>
import { ref } from 'vue'


    const name = ref('Jane Doe');
    const status = ref('pending');
    const tasks =ref(['One', 'Two', 'Three']);
    const link = ref('https://google.com')
    const newTask = ref('') // empty string for the input 

    const addTask = () =>{
      if(newTask.value.trim() !== '') { // if the input is not empty
        tasks.value.push(newTask.value) // push the task to the array
        newTask.value = '' // empty the input after it is added
      }
    }

    const deleteTask = (index) =>{
      tasks.value.splice(index, 1)
    }

    const changeStatus = () => {
      if (status.value === 'active') {
        status.value = 'pending'
      } else if (status.value === 'pending'){
        status.value = 'inactive'
      } else {
        status.value = 'active'
      }
      
    };


</script>

<template>
  <h1>{{name}}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else-if="status === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>

  <!-- v-on:submit  -->
  <!-- .prevent is for e.prevent default so the form wont submit  -->
  <form @submit.prevent="addTask">
    <label for="newTask">Add Task </label>
    <!-- v-model is for the state in the data section (in the script) -->
    <input type="text" id="newTask" name="newTask" v-model="newTask" />
    <button type="submit">Submit</button>
  </form>


  <h3>Tasks:</h3>
  <Ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>  
        {{ task }} 
        <button @click="deleteTask(index)">X</button>
      </span>
      </li>
  </Ul>
  <a :href="link">Click for Google</a>
  <br/>
  <!-- v-on:click="handler" or with the shortcut, @click="handler" -->
  <button @click="changeStatus">Change Status</button> 
</template>



<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #3c8ddd;
  margin-top: 60px;
}
</style>
