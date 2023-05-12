<script setup>

import { ref } from 'vue';

let todos =ref (['A','B','C'])
let newTodo =ref('')

function jim() {
todos.value.push({
text: newTodo.value,
complete:false
})


newTodo.value=''
}

function trash(index) {
todos.value.splice(index,1)


}
 
</script>

<template>
  <h1> My Todo Application</h1>

  <ul>
  <li v-for="(todo,index) in todos">
    <input type="checkbox" v-model="todo.complete">
    <button @click="trash(index)">trash</button>
   {{ todo.text }}  
  </li>
  </ul>
  <input v-model="newTodo" @keydown.enter="jim">
  <button @click="jim"> Add todo</button>

</template>

<style>

button{

background-color:#6246ea;
color: #fffffe;
text-align: center;
border-radius: 4px;
border-style: none;
font-size: 16px;
padding: 8px 16px;
margin: 2px 0;
cursor: pointer;
}

.center {
text-align: center;
}



h1{

color: black;
}

body{

  background-color: #abd1c6;

  text-align: center;
}

button:disabled {
background-color: gray;
cursor: not-allowed;
}



li{

color: white;
} 

</style>
