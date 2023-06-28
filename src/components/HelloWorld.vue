<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>
  </form>
  <ul>
    <li v-for="todo in todos" :key="todo">
      <span class="todo-item">{{ todo.text }}</span>
      <button @click="editTodo(todo)">edit</button>
      <button @click="updateTodo(todo)">update</button>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>
  <todoItem :todos="todos"/>
 
</template>

<script setup>
import todoItem from '@/components/todoItem.vue'
import { ref } from 'vue'

const newTodo = ref('')

const todos = ref([])

function addTodo() {
  todos.value.push({ text: newTodo.value})
  newTodo.value = ''
}
function editTodo(todo){
  newTodo.value=todo.text
}
function updateTodo(todo){
  todo.text=newTodo.value
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>



<style>
.todo-item{
  font-size: 25px;
}
input{
  padding-block: 5px;
  padding-left: 8px;
  border-radius: 5px;
}
button{
  padding-inline: 20px;
  padding-block: 5px;
  color:white;
  background-color: blue;
  border-radius: 5px;
  margin: 5px 10px;
}
</style>
