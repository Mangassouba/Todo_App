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
    <button class="add">Add New Todo</button>
  </form>
  <button class="rall" @click="removeAllTodos">Remove All</button>
  <button class="mall" @click="markAllDone">Mark All Done</button>
  <ul>
    <li v-for="(todo,index) in todos" v-bind:="todo.id" class="todo">
    <h3 :class="{ done : todo.done}" @click="toggleDone(todo)"> Todo{{ todo.content }}</h3>
    <button @click="removeTodo(index)">Remove Todo</button>
  </li>
  </ul>
 
  </div>
 
</template>

<style scoped>


/* input, textarea, button, p, div, section, article, select{
  display: block;
  width: 60%;
  font-family: sans-serif;
  font-size: 1em;
  margin: 0.5em;
} */
.add{
  background-color: green;
  color: #fff;
}
.rall{
  background-color: red;
  color: #fff;
}
.mall{
  background-color: blue;
  color: #fff;
}
input{
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
}
form button{
  width: 100%;
  margin: 0;
}

button{
  width: 60%;
  margin: 0.5em;
  padding: 10px;
}
form{
  width: 60%;
  display: flex;
  flex-direction: column;
}
/* form input */
.container{
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 60%;
  border: 1px solid #000;
  background-color: darkgrey;
}

.todo{
  cursor: pointer;
}

.done {
  text-decoration: line-through;
}

</style>
