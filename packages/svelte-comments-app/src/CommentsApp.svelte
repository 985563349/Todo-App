<script>
  import CommentBox from './lib/CommentBox.svelte';
  import DividerHorizontal from './lib/DividerHorizontal.svelte';
  import CommentItem from './lib/CommentItem.svelte';
  import ReplyContainer from './lib/ReplyContainer.svelte';
  import ReplyBox from './lib/ReplyBox.svelte';

  import face1 from './assets/logo.png';

  let rid = 4;

  let comments = [
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
  ];

  function constructNewComment(content) {
    return {
      id: rid,
      user: '当前用户',
      avatar: face1,
      time: '1秒前',
      content,
    };
  }

  function addNewComment(event) {
    const comment = constructNewComment(event.detail);
    comments.push(comment);
    comments = comments;
    rid++;
  }

  function addReplie(id, content) {
    const replie = constructNewComment(content);
    const comment = comments.find((comment) => comment.id === id);
    if (comment.replies) {
      comment.replies.push(replie);
    } else {
      comment.replies = [replie];
    }
    comments = comments;
  }
</script>

<main class="p-4 min-h-screen bg-gray-50">
  <div class="mx-auto p-8 max-w-screen-xl rounded-lg bg-white shadow-2xl">
    <h2 class="my-6 text-3xl">评论</h2>

    <CommentBox on:submit={addNewComment} />
    <DividerHorizontal />

    {#each comments as comment (comment.id)}
      <div>
        <CommentItem {...comment} />

        {#if comment.replies}
          <ReplyContainer>
            {#each comment.replies as replie (replie.id)}
              <CommentItem {...replie} />
            {/each}
          </ReplyContainer>
        {/if}

        <ReplyBox on:submit={(event) => addReplie(comment.id, event.detail)} />
      </div>
    {/each}
  </div>
</main>
