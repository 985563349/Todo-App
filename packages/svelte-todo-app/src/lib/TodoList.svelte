<script>
  import { createEventDispatcher } from 'svelte';
  import TodoItem from './TodoItem.svelte';

  const dispatch = createEventDispatcher();

  export let todos;
</script>

<div class="todo-list">
  {#each todos as todo (todo.id)}
    <TodoItem
      todoItem={todo}
      on:change-state={(event) => {
        dispatch('changeTodo', {
          id: todo.id,
          todo: { ...todo, completed: event.detail.target.checked },
        });
      }}
    />
  {/each}
</div>

<style>
  .todo-list {
    display: grid;
    row-gap: 14px;
  }
</style>
