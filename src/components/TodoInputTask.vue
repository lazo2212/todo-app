<script setup>
import { ref, defineProps } from 'vue';

let todoInputText = ref('');

defineProps({
  colorTheme: Object,
  addTodo: Function,
});
</script>

<template>
  <div class="container mb-3">
    <form class="input-group">
      <input
        type="text"
        class="form-control"
        placeholder="Add todo..."
        v-model="todoInputText"
      />
      <button
        :class="`btn btn-${colorTheme.btnClr}`"
        type="button"
        @click.prevent="
          () => {
            addTodo(todoInputText);
            todoInputText = '';
          }
        "
      >
        Add
      </button>
    </form>
  </div>
</template>

<style scoped>
.form-control:focus {
  border-color: #333;
  box-shadow: inset 0 0 1px #333, 0 0 8px #333;
}

@media (min-width: 992px) {
  .container {
    width: 50vw;
  }
}
</style>
