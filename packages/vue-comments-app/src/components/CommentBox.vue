<script setup>
import { ref } from 'vue';

const emit = defineEmits(['submit', 'cancel']);
const content = ref('');

const handleSubmit = (event) => {
  event.preventDefault();
  emit('submit', content.value);
  content.value = '';
};
</script>

<template>
  <form
    action=""
    class="grid"
    @submit="handleSubmit"
    @reset="emit('cancel', $event)"
  >
    <textarea
      v-model="content"
      class="p-2 rounded bg-gray-50"
      name="comment"
      placeholder="请输入评论"
    />
    <fieldset class="py-4">
      <button class="px-4 py-1 rounded bg-blue-600 text-white" type="submit">
        评论
      </button>
      <button type="reset" class="ml-3 border px-4 py-1 rounded bg-white">
        取消
      </button>
    </fieldset>
  </form>
</template>
