<template>
  <div class="ms-24 mt-24">
  <form @submit.prevent="addTodo">
    <input class="border border-2 border-red-400 rounded py-2 ps-3" placeholder="Enter user name" v-model="newTodo">
    <button class="ms-5 px-3 py-1 border border-2 border-blue-400 bg-green-300 rounded">Add Todo</button>
  </form>

  <table>
    <th>
      <h1 class="text-3xl mt-5 mb-5 p-2 bg-purple-500 rounded text-white">Todo List</h1>
    </th>
    <tr v-for="todo in todos" :key="todo">
      <td><span class="todo-item">{{ todo.text }}</span></td>
      <td><button class="mx-10 px-3 py-1 border border-2 border-green-400 bg-purple-300 rounded" @click="editTodo(todo)">edit</button></td>
      <td><button class="mx-10 px-3 py-1 border border-2 border-green-400 bg-orange-300 rounded" @click="updateTodo(todo)">update</button></td>
      <td><button class="mx-10 px-3 py-1 border border-2 border-green-400 bg-red-300 rounded" @click="removeTodo(todo)">X</button></td>
      
    </tr>
  </table>
  
  <todoItem :todos="todos"/>
</div>
<hr class="my-10">
</template>

<script setup>
import todoItem from '@/components/todoItem.vue'
import { ref } from 'vue'

const newTodo = ref('')

const todos = ref([])

function addTodo() {
  if(newTodo.value.trim()!==''){
    todos.value.push({ text: newTodo.value})
    newTodo.value = ''
  }
 
}
function editTodo(todo){
  newTodo.value=todo.text
}
function updateTodo(todo){
  todo.text=newTodo.value;
  newTodo.value = '';
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
/* button{
  padding-inline: 20px;
  padding-block: 5px;
  color:white;
  background-color: rgb(62, 62, 134);
  border-radius: 5px;
  margin: 5px 10px;
} */
</style>
