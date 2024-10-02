<script>
import HelloWorld from './components/HelloWorld.vue'
function randomNum(){
  return "Random number is #"+Math.floor(Math.random()*1000)
}
function name(){
  return "VUE JOBS"
}
export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data(){
    return {
      title: randomNum(),
      name: name(),
      status: true,
      activation: "active",

      tasks: ["one", "two", "three"],

      link: 'https://google.com',
    }
  },
  methods: {
    toggleStatus(){
      if(this.activation === 'active'){
        this.activation = 'pending'
      } else if(this.activation === 'pending'){
        this.activation = 'inactive'
      } else {
        this.activation = 'active'
      }
    },
  },
}

</script>

<template>
  <!-- from the component  -->
  <HelloWorld msg="Vue Jobs"/>


  <h2>{{title}}</h2>
  <h1>{{name}}</h1>
  <!-- if else  -->
  <p v-if="status">User has status</p>
  <p v-if="activation === 'active'">User is active</p>
  <p v-else-if="activation === 'pending'">User is pending</p>
  <p v-else>User is inactive</p>

<!-- for loop -->
  <h3> Tasks:</h3>
    <ul>
      <li v-for="task in tasks" :key="task">{{ task }}</li>
    </ul>

    <!-- bind -->
    <!-- <a v-bind:href="link">click for google</a> --> 
    <!-- shortest way of doing bind -->
    <a :href="link">click for google</a>

    <!-- events -->
    <br>
    <!-- <button v-on:click="toggleStatus">change status</button> -->
    <!-- shortest way of doing event handles -->
    <button @click="toggleStatus">change status</button>
</template>



<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: blueviolet;
  margin-top: 60px;
}
</style>
