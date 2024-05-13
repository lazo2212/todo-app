<script setup>
import { reactive, onMounted } from 'vue';
import Header from './components/Header.vue';
import TodoInputTask from './components/TodoInputTask.vue';
import TodoList from './components/TodoList.vue';

// *****  THEME LOGIC *****
let colorTheme = reactive({
  themeClr: 'dark',
  textClr: 'light',
  btnClr: 'light',
});

onMounted(() => {
  getTheme();
  getTodos();
});

function getTheme() {
  let theme = JSON.parse(localStorage.getItem('colorTheme'));
  Object.assign(colorTheme, theme);
}

function setTheme() {
  localStorage.setItem('colorTheme', JSON.stringify(colorTheme));
}

function toggleTheme() {
  colorTheme.themeClr = colorTheme.themeClr === 'dark' ? 'light' : 'dark';
  colorTheme.textClr = colorTheme.textClr === 'dark' ? 'light' : 'dark';
  colorTheme.btnClr = colorTheme.btnClr === 'dark' ? 'light' : 'dark';

  setTheme();
}
//  *****  TODO TASKS LOGIC  *****
const todos = reactive([]);

function getTodos() {
  let newTodos = JSON.parse(localStorage.getItem('todos'));
  Object.assign(todos, newTodos);
}

function setTodos() {
  localStorage.setItem('todos', JSON.stringify(todos));
}

function addTodo(todoInputText) {
  if (todoInputText === '') {
    return;
  }

  todos.push({ text: todoInputText });
  setTodos();
}

function deleteTodo(index) {
  todos.splice(index, 1);
  setTodos();
}
</script>

<template>
  <div
    class="fullScreen"
    :class="`bg-${colorTheme.themeClr} text-${colorTheme.textClr}`"
  >
    <Header :color-theme="colorTheme" :toggle-theme="toggleTheme"></Header>

    <TodoInputTask
      :color-theme="colorTheme"
      :add-todo="addTodo"
    ></TodoInputTask>

    <TodoList :todos="todos" :delete-todo="deleteTodo"></TodoList>
  </div>
</template>

<style>
.fullScreen {
  min-height: 100vh;
  min-width: 100vw;
}
</style>
