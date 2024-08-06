<script>
import {ref, reactive } from "vue";
export default{
setup(){


  const newTodo = ref(''); 
  const todos = ref([]);
  function addNewtodo(){

    todos.value.push({
      // id : Data.now(),
      done : false,
      content : newTodo.value
    });
  // console.log(newTodo.value)
  newTodo.value = '';
}

function toggleDone(todo) {
  todo.done = !todo.done;
}

function removeTodo(index){
  todos.value.splice(index, 1)
}

function markAllDone() {
  todos.value.forEach((todo) => todo.done = true);
}

function removeAllTodos(){
  todos.value = [];
}


return {
  todos,
  newTodo,
  addNewtodo,
  toggleDone,
  removeTodo,
  markAllDone,
  removeAllTodos
}
}
}


</script>

<template>

  <div class="container">
    <h1>Vue 3 Todo App</h1>
  <form @submit.prevent="addNewtodo">
    <label for="">New todo</label>
    <input v-model="newTodo" name="newTodo">
    <button>Add New Todo</button>
  </form>
  <button @click="removeAllTodos">Remove All</button>
  <button @click="markAllDone">Mark All Done</button>
  <ul>
    <li v-for="(todo,index) in todos" v-bind:="todo.id" class="todo">
    <h3 :class="{ done : todo.done}" @click="toggleDone(todo)"> Todo{{ todo.content }}</h3>
    <button @click="removeTodo(index)">Remove Todo</button>
  </li>
  </ul>
 
  </div>
 
</template>

<style scoped>
body{
  font-family: sans-serif;
  padding-top: 1em;
  padding-bottom: 1em;
  font-size: 2em;
  width: 80%;
  margin: 0 auto;
}

input, textarea, button, p, div, section, article, select{
  display: block;
  width: 100%;
  font-family: sans-serif;
  font-size: 1em;
  margin: 0.5em;
}

.container{
  width: 50%;
}

.todo{
  cursor: pointer;
}

.done {
  text-decoration: line-through;
}

</style>
