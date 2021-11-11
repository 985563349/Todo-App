<script setup>
import { ref } from 'vue';

import CommentBox from './components/CommentBox.vue';
import DividerHorizontal from './components/DividerHorizontal.vue';
import CommentItem from './components/CommentItem.vue';
import ReplyContainer from './components/ReplyContainer.vue';
import ReplyBox from './components/ReplyBox.vue';

import face1 from './assets/logo.png';

const rid = ref(4);

const comments = ref([
  {
    id: 1,
    user: '梦落轻寻',
    avatar: face1,
    time: '2小时之前',
    content:
      '哇！这篇文章真的写的太好啦！收到很大的启发，希望博主能够再接再厉，产出越来越多，越来越好的文章！凑字数，字数，....',
    replies: [
      {
        id: 2,
        user: '陌上开花',
        avatar: face1,
        time: '2小时之前',
        content: '赞！',
      },
      {
        id: 3,
        user: '半梦半醒半浮生',
        avatar: face1,
        time: '2小时之前',
        content:
          '哇！这篇文章真的写的太好啦！收到很大的启发，希望博主能够再接再厉，产出越来越多，越来越好的文章！凑字数，字数，....',
      },
    ],
  },
]);

const constructNewComment = (content) => {
  return {
    id: rid.value,
    user: '当前用户',
    avatar: face1,
    time: '1秒前',
    content,
  };
};

const addNewComment = (content) => {
  const newComment = constructNewComment(content);
  comments.value.push(newComment);
  rid.value++;
};

const addReply = (content, id) => {
  const reply = constructNewComment(content);
  const comment = comments.value.find((comment) => comment.id === id);
  if (comment.replies) {
    comment.replies.push(reply);
  } else {
    comment.replies = [reply];
  }
};
</script>

<template>
  <main class="p-4 min-h-screen bg-gray-50">
    <div class="mx-auto p-8 max-w-screen-xl rounded-lg bg-white shadow-2xl">
      <h2 class="text-3xl my-6">评论</h2>
      <comment-box @submit="addNewComment" />
      <divider-horizontal />

      <div v-for="comment of comments" :key="comment.id">
        <comment-item
          :name="comment.user"
          :avatar="comment.avatar"
          :time="comment.time"
          :content="comment.content"
        />

        <reply-container v-if="comment.replies">
          <comment-item
            v-for="replie of comment.replies"
            :key="replie.id"
            :name="replie.user"
            :avatar="replie.avatar"
            :time="replie.time"
            :content="replie.content"
          />
        </reply-container>

        <reply-box @submit="addReply($event, comment.id)" />
      </div>
    </div>
  </main>
</template>
