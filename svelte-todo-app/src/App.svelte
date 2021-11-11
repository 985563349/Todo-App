<script>
  import { onMount } from 'svelte';
  import TodoAdd from './lib/TodoAdd.svelte';
  import TodoFilter from './lib/TodoFilter.svelte';
  import TodoList from './lib/TodoList.svelte';

  let todos = [];

  function addTodo(event) {
    todos = todos.concat(event.detail);
  }

  function changeTodo(event) {
    const index = todos.findIndex((todo) => todo.id === event.detail.id);
    if (index !== -1) {
      todos[index] = event.detail.todo;
      // 赋值操作触发更新
      todos = todos;
    }
  }

  async function fetchTodos() {
    const response = await fetch(
      'https://jsonplaceholder.typicode.com/todos?_limit=5'
    );
    const rawTodos = await response.json();
    todos = rawTodos.map((todo, index) => ({
      id: index,
      content: todo.title,
      completed: todo.completed,
    }));
  }

  onMount(fetchTodos);

  let filter = 'all';
  let filteredTodos;

  $: {
    switch (filter) {
      case 'done':
        filteredTodos = todos.filter((todo) => todo.completed);
        break;
      case 'todo':
        filteredTodos = todos.filter((todo) => !todo.completed);
        break;
      default:
        filteredTodos = todos;
    }
  }
</script>

<main>
  <div class="container">
    <h1>欢迎使用待办列表！</h1>
    <TodoAdd tid={todos.length} on:addTodo={addTodo} />
    <TodoFilter
      selected={filter}
      on:changeFilter={(evnet) => (filter = evnet.detail)}
    />
    <TodoList todos={filteredTodos} on:changeTodo={changeTodo} />
  </div>
</main>

<style>
  :global(*) {
    box-sizing: border-box;
    margin: 0px;
    padding: 0px;
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
