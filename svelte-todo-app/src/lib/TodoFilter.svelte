<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  export let selected;

  const filters = [
    { label: '全部', value: 'all' },
    { label: '已完成', value: 'done' },
    { label: '未完成', value: 'todo' },
  ];
</script>

<div class="filters">
  {#each filters as filter (filter.value)}
    <span
      class="filter"
      class:active={selected === filter.value}
      on:click={() => dispatch('changeFilter', filter.value)}
    >
      {filter.label}
    </span>
  {/each}
</div>

<style>
  .filters {
    display: flex;
    margin: 24px 2px;
    color: #c0c2ce;
    font-size: 14px;
  }

  .filters .filter {
    margin-right: 14px;
    transition: 0.8s;
    cursor: pointer;
  }

  .filters .filter.active {
    color: #6b729c;
    transform: scale(1.2);
  }
</style>
