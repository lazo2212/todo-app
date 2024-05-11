<script setup>
import { ref, reactive, onMounted } from 'vue';
import Header from './components/Header.vue';
import TodoInputTask from './components/TodoInputTask.vue';

// *****  THEME LOGIC *****
let colorTheme = reactive({
  themeClr: 'dark',
  textClr: 'light',
  btnClr: 'light',
});

onMounted(() => getTheme());

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
const todos = reactive([
  { id: 1, text: 'Prvi zadatak' },
  { id: 2, text: 'Drugi zadatak' },
]);

function addTodo(todoInputText) {
  if (todoInputText === '') {
    return;
  }

  todos.push({ id: todos.length, text: todoInputText });
}
</script>

<template>
  <div
    class="vw-100 vh-100"
    :class="`bg-${colorTheme.themeClr} text-${colorTheme.textClr}`"
  >
    <Header :color-theme="colorTheme" :toggle-theme="toggleTheme"></Header>
    <TodoInputTask
      :color-theme="colorTheme"
      :add-todo="addTodo"
    ></TodoInputTask>

    <div class="container">
      <ul class="list-group">
        <li
          class="list-group-item d-flex justify-content-between"
          v-for="todo in todos"
          :key="todo.id"
        >
          {{ todo.text }}
          <button class="btn btn-sm btn-danger text-weight-bold">X</button>
        </li>
      </ul>
    </div>
  </div>
</template>
