<script setup>


import { ref, watch } from 'vue';

let todos = ref(JSON.parse(window.localStorage.getItem('todos'))?? [])
let newTodo = ref('')
let filter = ref('all')

watch(todos, function (value) {
  window.localStorage.setItem('todos', JSON.stringify(value))
}, { deep: true })

function jim() {
  todos.value.push({
    text: newTodo.value,
    complete: false
  })

  newTodo.value = ''
}

function trash(index) {
  todos.value.splice(index, 1)
}



function todoFilter(todo) {
  if (filter.value == 'active') {
    return todo.complete == false
  } else if (filter.value == 'complete') {
    return todo.complete == true
  } else {
    return true
  }
}

function activeFilter(todo) {
  return todo.complete == false
}

</script>

<template>
  <h1> My Todo Application</h1>

  <p v-if="todos.length > 0">
  </p>

  <p> {{ todos.filter(activeFilter).length}} items left</p>
  <p>
    <input name="filter" type="radio" value="all" v-model="filter">
    <label>All</label>

    <input name="filter" type="radio" value="active" v-model="filter">
    <label>Active</label>

    <input name="filter" type="radio" value="complete" v-model="filter">
    <label>Complete</label>

  </p>
  <input   v-model="newTodo" @keydown.enter="jim" placeholder=" Press enter to add to list">
  
  <ul>
    <li v-for="(todo, index) in todos.filter(todoFilter)" :class="{ completed: todo.complete }">
      <input type="checkbox" v-model="todo.complete">
      <button @click="trash(index)">🗑️</button>
      {{ todo.text }}
    </li>
  </ul>

</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Bree+Serif&display=swap');

@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap');







input{
  font-size: 25px;
  border-radius: 25px;
  background-color: #eebbc3;
}

li {

  color: black;

}

button {

  background-color: grey;
  color: black;
  text-align: center;
  border-radius: 4px;
  border-style: none;
  font-size: 20px;
  padding: 8px 16px;
  margin: 2px 0;
  cursor: pointer;
  height: 50px;
  width: 50px;
}

.center {
  text-align: center;
}


h1 {

  color: black;
  font-family: 'Bebas Neue';
}

body {

  
  background-color: #b8c1ec;

  text-align: center;

  font-style: 'Bebas Neue';

  color: black;
}

button:disabled {
  background-color: #f25f4c;
  cursor: not-allowed;
}



input[type="checkbox"] {

  border-radius: 50px;
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
  font-size: 25px;
}

input[type="checkbox"]::after {
  font-family: "Font Awesome 5 Free";
  content: "\f00c";
  font-weight: 900;
  font-size: 50px;
  color: white;
  display: none;
}

input[type="checkbox"]:hover {
  background-color: #a5a5a5;
}

input[type='checkbox']:checked {
  background-color: #5bcd3e;

  
}

input[type="checkbox"]:checked::after {
  display: block
  
}
</style>
