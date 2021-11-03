<script>
  import TodoItem from './TodoItem.svelte';

  export let todos;
</script>

<div class="todo-list">
  {#each todos as todo (todo.id)}
    <TodoItem
      todoItem={todo}
      on:change-state={(event) => {
        todo.completed = event.detail.target.checked;
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
