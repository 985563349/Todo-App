<script setup>
import { ref } from 'vue';
import CommentBox from './CommentBox.vue';

const emit = defineEmits(['submit']);
const showCommentBox = ref(false);
</script>

<template>
  <button
    class="pt-4 text-blue-600"
    :class="[showCommentBox ? 'pb-2' : 'pb-10']"
    @click="showCommentBox = !showCommentBox"
  >
    回复
  </button>
  <comment-box
    v-if="showCommentBox"
    class="mb-4"
    @submit="
      emit('submit', $event);
      showCommentBox = false;
    "
    @cancel="showCommentBox = false"
  />
</template>
