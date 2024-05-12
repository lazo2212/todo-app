<script setup>
import { defineProps } from 'vue';

defineProps({
  todos: Array,
  deleteTodo: Function,
});
</script>

<template>
  <div class="container">
    <ul class="list-group">
      <li
        class="list-group-item d-flex justify-content-between"
        v-for="(todo, index) in todos"
        :key="index"
      >
        {{ todo.text }}
        <button
          class="btn btn-sm btn-danger text-weight-bold"
          @click="deleteTodo(index)"
        >
          X
        </button>
      </li>
    </ul>
  </div>
</template>
