<script setup>
import TodoAdd from './components/TodoAdd.vue';
import TodoFilter from './components/TodoFilter.vue';
import TodoList from './components/TodoList.vue';
import useTodos from './composables/useTodos';
import useFilteredTodos from './composables/useFilteredTodos';

const { todos, addTodo } = useTodos();
const { filter, filteredTodos } = useFilteredTodos(todos);
</script>

<template>
  <main>
    <div class="container">
      <h1>欢迎使用待办事项！</h1>
      <todo-add :tid="todos.length" @add-todo="addTodo" />
      <todo-filter :selected="filter" @change-filter="filter = $event" />
      <todo-list :todos="filteredTodos" />
    </div>
  </main>
</template>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Helvetica, 'PingFang SC', 'Microsoft Yahei', sans-serif;
}

main {
  width: 100vw;
  min-height: 100vh;
  display: grid;
  align-items: center;
  justify-items: center;
  background-color: rgb(203, 210, 240);
}

.container {
  width: 60%;
  max-width: 400px;
  box-shadow: 0px 0px 24px rgba(0, 0, 0, 0.15);
  border-radius: 24px;
  padding: 48px 28px;
  background-color: rgb(245, 246, 252);
}

h1 {
  margin: 24px 0;
  font-size: 28px;
  text-align: center;
  color: #414873;
}
</style>
