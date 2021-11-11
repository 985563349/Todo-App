<script setup>
import TodoItem from './TodoItem.vue';

defineProps({ todos: Array });
</script>

<template>
  <div class="todo-list">
    <todo-item
      v-for="todo of todos"
      :key="todo.id"
      :todo-item="todo"
      @change-state="todo.completed = $event.target.checked"
    />
  </div>
</template>

<style scoped>
.todo-list {
  display: grid;
  row-gap: 14px;
}
</style>
