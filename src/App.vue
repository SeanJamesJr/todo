<script setup>


import { ref,watch } from 'vue';

let todos =ref (JSON.parse(window.localStorage.getItem('todos')))
let newTodo =ref('')

watch(todos, function(value){
window.localStorage.setItem('todos',JSON.stringify(value))
}, {deep: true})

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

  <head><link rel="stylesheet"
     href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  </head>
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

@import url();

button{

background-color:#ff8906;
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

color: #fffffe;
}

body{

  background-color: #0f0e17;

  text-align: center;

  font-style: Bebas Neue;
}

button:disabled {
background-color: #f25f4c;
cursor: not-allowed;
}

input[type="checkbox"]{
appearance: none;
-webkit-appearance: none;
height: 20px;
width: 20px;
background-color: #fffffe;
border-radius: 5px;
cursor: pointer;

}


li{

color: white;
} 

input [type="checkbox"]::after{

  content:"\f14a";
}

</style>
