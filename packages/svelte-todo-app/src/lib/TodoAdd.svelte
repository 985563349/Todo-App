<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  export let tid;

  let todoContent = '';

  function emitAddTodo() {
    const todo = {
      id: tid,
      content: todoContent,
      completed: false,
    };
    dispatch('addTodo', todo);
    todoContent = '';
  }
</script>

<div class="input-add">
  <input
    type="text"
    bind:value={todoContent}
    on:keyup={(event) => {
      if (event.key === 'Enter') emitAddTodo();
    }}
  />
  <button on:click={emitAddTodo}>
    <i class="plus" />
  </button>
</div>

<style>
  .input-add {
    position: relative;
    display: flex;
    align-items: center;
  }

  .input-add input {
    padding: 16px 52px 16px 18px;
    border-radius: 48px;
    border: none;
    outline: none;
    box-shadow: 0px 0px 24px rgba(0, 0, 0, 0.08);
    width: 100%;
    font-size: 16px;
    color: #626262;
  }

  .input-add button {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    background: linear-gradient(#c0a5f3, #7f95f7);
    border: none;
    outline: none;
    color: #fff;
    position: absolute;
    right: 0px;
    cursor: pointer;
  }

  .input-add .plus {
    display: block;
    width: 100%;
    height: 100%;
    background: linear-gradient(#fff, #fff), linear-gradient(#fff, #fff);
    background-size: 50% 2px, 2px 50%;
    background-position: center;
    background-repeat: no-repeat;
  }
</style>
