<template>
  <main class="form">
    <h2>Class shopping cart</h2>
    <p>
      Here you can make a list of classes you are planning on taking.
    </p>

    <form @submit.prevent="createTodo" class="create-todo">
      <label for="todo">Class:</label>
      <select v-model="selectedClass">
        <option v-for="course in courseList" :key="course">{{ course }}</option>
      </select>
      <button type="submit">Save</button>
    </form>

    <ul>
      <li v-for="(todo, index) in todos" :key="index">
        {{ todo }}
        <button @click="deleteTodo(index)">Delete</button>
      </li>
    </ul>
  </main>
</template>

<script setup>
import { ref } from "vue";

const selectedClass = ref(""); // Store the selected class
const courseList = ref([
  'CSE1010', 'CSE2050', 'CSE2102', 'MATH1030Q', 'MATH1060Q', 'MATH1151Q', // Add more classes
]);
const todos = ref([]); // Store the saved classes

function createTodo() {
  if (selectedClass.value && !todos.value.includes(selectedClass.value)) {
    todos.value.push(selectedClass.value);
  }
}

function deleteTodo(index) {
  todos.value.splice(index, 1);
}
</script>

<style>
.form {
  padding: 1rem;
}

.form h2 {
  font-size: 1.5rem;
  margin-bottom: 2rem;
}

.form p {
  margin-bottom: 1rem;
}

/* flex layouts allow us to position elements next to each other that would otherwise have been on top of each other */
.form ul {
  display: flex;
  gap: 1rem;
  flex-direction: column;
}
.form li {
  display: flex;
  gap: 0.5rem;
  align-items: center;
}

/* create some space beneath the create todo form */
.form form {
  margin-bottom: 1rem;
}

/* set some default styling to buttons and inputs for borders, heights, and padding */
.form :is(input, button) {
  line-height: 2rem;
  padding-inline: 0.5rem;
  border-radius: 0.375rem;
  border: 1px solid #d9d9d9;
  margin-left: 0.5rem;
  color: #202020;
}
</style>

