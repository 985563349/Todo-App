<script>
  import { createEventDispatcher } from 'svelte';
  import CommentBox from './CommentBox.svelte';

  const dispatch = createEventDispatcher();

  let showCommentBox = false;
</script>

<button
  class="pt-4 text-blue-600 {showCommentBox ? 'pb-2' : 'pb-10'}"
  on:click={() => (showCommentBox = !showCommentBox)}
>
  回复
</button>
{#if showCommentBox}
  <CommentBox
    on:submit={(event) => dispatch('submit', event.detail)}
    on:reset={() => (showCommentBox = false)}
  />
{/if}
