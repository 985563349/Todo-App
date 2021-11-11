<script>
  import { createEventDispatcher } from 'svelte';
  const dispatch = createEventDispatcher();

  let content = '';

  function handleSubmit(event) {
    event.preventDefault();
    dispatch('submit', content);
    content = '';
  }
</script>

<form class="grid" on:submit={handleSubmit} on:reset={() => dispatch('reset')}>
  <textarea
    class="p-2 bg-gray-50"
    bind:value={content}
    placeholder="请输入评论"
  />
  <fieldset class="py-4">
    <button type="submit" class="px-4 py-1 rounded bg-blue-600 text-white">
      评论
    </button>
    <button type="reset" class="ml-2 border px-4 py-1 rounded bg-white">
      取消
    </button>
  </fieldset>
</form>
