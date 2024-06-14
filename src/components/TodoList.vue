<script setup lang="ts">
import { ref } from "vue"

interface Todo{
  name: string
}
const todos = ref<Todo[]>([
  {name: "数学"}
])

const dones = ref<Todo[]>([
  {name: "英語"}
])

const newTodo = ref("")

function addTodo () {
  todos.value.push({name: newTodo.value})
}

function removeTodo(todo:Todo){
  todos.value = todos.value.filter((t) => t !== todo)
}

function makeDone (todo:Todo) {
  dones.value.push({name: todo.name})
  removeTodo(todo)
}

</script>

<template>
  <h1>TodoList</h1>
  <b>--やることリスト--</b>
  <ul>
    <li v-for="todo in todos" :key="todo.name">
      <div class="a">やること：{{ todo.name }}</div>
      <button v-on:click="makeDone(todo)">完了！</button>
    </li>
  </ul>
  <input type="text" v-model="newTodo">
  <button v-on:click="addTodo">追加</button><br>
  <b>--完了済みリスト--</b>
  <ul>
    <li v-for="done in dones" :key="done.name">
      <div class="b">したこと：{{ done.name }}</div>
    </li>
  </ul>
</template>

<style>
  .a{
    color:red
  }
  .b{
    color:gray
  }
</style>