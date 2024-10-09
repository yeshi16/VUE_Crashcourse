<script setup>
import { ref, onMounted } from "vue";

const tasks = ref(["One", "Two", "Three"]);

const newTask = ref(""); // empty string for the input

const addTask = () => {
  if (newTask.value.trim() !== "") {
    // if the input is not empty
    tasks.value.push(newTask.value); // push the task to the array
    newTask.value = ""; // empty the input after it is added
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

onMounted(async()=>{
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await response.json()
    // console.log(data)
    tasks.value = data.map((task) => task.title) // get title only from fetched data

  } catch (error) {
    console.log('Error fetching tasks')
  }
})
</script>

<template>

<form @submit.prevent="addTask">
  <h1>Tasks</h1>
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
  
  

</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #4d6728;
  margin-top: 60px;
  margin-left: 20px;
}
</style>
