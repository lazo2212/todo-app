<script setup>
import { defineProps } from 'vue';

defineProps({
  todos: Array,
  isFinished: Function,
  deleteTodo: Function,
});
</script>

<template>
  <div class="container">
    <ul class="list-group">
      <li
        class="list-group-item d-flex justify-content-between"
        :class="
          todo.finished ? 'text-decoration-line-through text-success' : ''
        "
        v-for="(todo, index) in todos"
        :key="index"
      >
        {{ todo.text }}

        <div>
          <button
            class="btn btn-sm btn-success text-weight-bold me-1"
            @click="isFinished(index)"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="16"
              height="16"
              fill="currentColor"
              class="bi bi-check2"
              viewBox="0 0 16 16"
            >
              <path
                d="M13.854 3.646a.5.5 0 0 1 0 .708l-7 7a.5.5 0 0 1-.708 0l-3.5-3.5a.5.5 0 1 1 .708-.708L6.5 10.293l6.646-6.647a.5.5 0 0 1 .708 0"
              />
            </svg>
          </button>
          <button
            class="btn btn-sm btn-danger text-weight-bold"
            @click="deleteTodo(index)"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="16"
              height="16"
              fill="currentColor"
              class="bi bi-x-lg"
              viewBox="0 0 16 16"
            >
              <path
                d="M2.146 2.854a.5.5 0 1 1 .708-.708L8 7.293l5.146-5.147a.5.5 0 0 1 .708.708L8.707 8l5.147 5.146a.5.5 0 0 1-.708.708L8 8.707l-5.146 5.147a.5.5 0 0 1-.708-.708L7.293 8z"
              />
            </svg>
          </button>
        </div>
      </li>
    </ul>
  </div>
</template>
