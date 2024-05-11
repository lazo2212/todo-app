<script setup>
import { defineProps } from 'vue';

defineProps({
  colorTheme: Object,
  toggleTheme: Function,
});
</script>

<template>
  <div
    class="container d-flex justify-content-between align-items-center pt-3 pb-3"
  >
    <h1 class="w-100 text-center">TO-DO APP</h1>
    <button :class="`btn btn-${colorTheme.btnClr}`" @click="toggleTheme">
      {{ colorTheme.themeClr === 'dark' ? 'Light' : 'Dark' }}
    </button>
  </div>
</template>
