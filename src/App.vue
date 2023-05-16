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

  <h1> My Todo Application</h1>

  <ul>
  <li v-for="(todo, index) in todos" :class= "{completed: todo.complete}" >
    <input type="checkbox" v-model="todo.complete">
    <button @click="trash(index)">🗑️</button>
   {{ todo.text }}  
  </li>
  </ul>
  <input v-model="newTodo" @keydown.enter="jim">
  <button @click="jim"> Add todo</button>

</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Bree+Serif&display=swap');

li{

color: white;
} 

button{

background-color:grey;
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
height: 50px;
width: 50px;
background-color: #d5d5d5;
border-radius: 5px;
cursor: pointer;
display: inline-flex;
align-items: center;
justify-content: center;
outline: none;
}

input[type="checkbox"]::after{

  font-family: "Font Awesome 5 Free";
  content:"\f00c";
  font-weight: 900;
  font-size: 50px;
  color: white;
  display: none;
}

input[type="checkbox"]:hover {
background-color: #a5a5a5;

}
input[type='checkbox']:checked{
background-color: #5bcd3e;

}

input[type="checkbox"]:checked::after {
display:block


}

</style>
