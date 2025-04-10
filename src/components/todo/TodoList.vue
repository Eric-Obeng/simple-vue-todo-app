<script setup lang="ts">
import { ref } from 'vue'
import type { Todo } from '@/types/todo'

const newTodo = ref('')
const todos = ref<Todo[]>([])

const addTodo = () => {
  if (newTodo.value.trim()) {
    todos.value.push({
      id: Date.now(),
      text: newTodo.value,
      completed: false,
    })
    newTodo.value = ''
  }
}

const toggleTodo = (todo: Todo) => {
  todo.completed = !todo.completed
}

const removeTodo = (id: number) => {
  todos.value = todos.value.filter((todo) => todo.id !== id)
}
</script>

<template>
  <div class="todo-container">
    <h1>Todo List</h1>

    <div class="add-todo">
      <input v-model="newTodo" @keyup.enter="addTodo" placeholder="Add a new todo" type="text" />
      <button @click="addTodo">Add</button>
    </div>

    <ul class="todo-list">
      <li v-for="todo in todos" :key="todo.id" :class="{ completed: todo.completed }">
        <input type="checkbox" :checked="todo.completed" @change="toggleTodo(todo)" />
        <span>{{ todo.text }}</span>
        <button @click="removeTodo(todo.id)" class="delete-btn">×</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.todo-container {
  margin-top: 2rem;
  padding: 1rem;
  max-width: 100%;
  margin-inline: auto;
}

.add-todo {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
  width: 100%;
}

.add-todo input {
  flex: 1;
  padding: 12px;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 16px;
}

button {
  padding: 12px 24px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 16px;
  transition: background-color 0.2s ease;
}

button:hover {
  background-color: #45a049;
}

.todo-list {
  list-style: none;
  padding: 0;
  width: 100%;
}

.todo-list li {
  display: flex;
  align-items: center;
  padding: 15px;
  margin: 8px 0;
  background-color: #f9f9f9;
  border-radius: 8px;
  gap: 15px;
  transition: transform 0.2s ease;
}

.todo-list li:hover {
  transform: translateX(5px);
}

.todo-list li.completed span {
  text-decoration: line-through;
  color: #888;
}

.delete-btn {
  background-color: #ff4444;
  width: 24px;
  height: 24px;
  margin-left: auto;
  font-size: 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0;
  border-radius: 4px;
  flex-shrink: 0;
}

.delete-btn:hover {
  background-color: #cc0000;
}

/* Modern Media Queries using Container Queries where supported */
@container (min-width: 768px) {
  .todo-container {
    padding: 2rem;
  }
}

/* Fallback Media Queries */
@media (max-width: 480px) {
  .todo-container {
    padding: 0.5rem;
  }

  .add-todo {
    flex-direction: column;
    gap: 8px;
  }

  button {
    width: 100%;
    padding: 10px;
  }

  .todo-list li {
    padding: 12px;
    font-size: 14px;
  }
}

@media (min-width: 481px) and (max-width: 768px) {
  .todo-container {
    padding: 1rem;
  }

  .todo-list li {
    padding: 12px;
  }
}

@media (min-width: 769px) {
  .todo-container {
    max-width: 1000px;
    margin: 2rem auto;
    padding: 2rem 3rem;
  }

  .todo-list li {
    padding: 1rem 2rem;
  }
}

/* Dark mode support */
@media (prefers-color-scheme: dark) {
  .todo-list li {
    background-color: #2a2a2a;
    color: #fff;
  }

  .add-todo input {
    background-color: #2a2a2a;
    color: #fff;
    border-color: #444;
  }

  .todo-list li.completed span {
    color: #666;
  }
}
</style>
