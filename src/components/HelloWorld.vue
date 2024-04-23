<script setup>
import { ref, onMounted } from "vue";

const todos = ref([]);
const text = ref("");

const deleteTodo = (todo) => {
  todos.value.pop(todo);
  saveTodosToLocalStorage();
};

const onSubmit = () => {
  todos.value.push(text.value);
  saveTodosToLocalStorage();
};

const saveTodosToLocalStorage = () => {
  localStorage.setItem("todos", JSON.stringify(todos.value));
};

onMounted(() => {
  const savedTodos = localStorage.getItem("todos");
  if (savedTodos) {
    todos.value = JSON.parse(savedTodos);
  }
});
</script>

<template>
  <form @submit.prevent="onSubmit">
    <input v-model="text" />
    <button type="submit">submit</button>
  </form>
  <li v-for="todo in todos" :key="todo.id">
    {{ todo }}
    {{ todo.id }}
    <button @click="deleteTodo(todo)">Delete</button>
  </li>
  <p>hello</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
