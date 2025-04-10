<script setup lang="ts">
import TodoList from './components/todo/TodoList.vue'
</script>

<template>
  <div class="app-container">
    <TodoList />
  </div>
</template>

<style scoped>
.app-container {
  width: 100%;
  padding: 20px;
  height: 100vh;
  margin-inline: auto;
}
</style>
