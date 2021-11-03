<script setup>
import { defineProps, defineEmits, ref } from 'vue';

const props = defineProps({ tid: String });
const emits = defineEmits(['add-todo']);

const { todoContent, emitAddTodo } = useEmitAddTodo(props.tid, emits);

function useEmitAddTodo(tid, emits) {
  const todoContent = ref('');

  const emitAddTodo = () => {
    const todo = {
      id: tid,
      content: todoContent.value,
      completed: false,
    };
    emits('add-todo', todo);
    todoContent.value = '';
  };

  return {
    todoContent,
    emitAddTodo,
  };
}
</script>

<template>
  <div class="input-add">
    <input
      type="text"
      name="todo"
      v-model="todoContent"
      @keyup.enter="emitAddTodo"
    />
    <button @click="emitAddTodo">
      <i class="plus"></i>
    </button>
  </div>
</template>

<style scoped>
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
