<script setup>
defineProps({ selected: String });

const filters = [
  { label: '全部', value: 'all' },
  { label: '已完成', value: 'done' },
  { label: '未完成', value: 'todo' },
];
</script>

<template>
  <div class="filters">
    <span
      v-for="filter of filters"
      :key="filter.value"
      @click="$emit('change-filter', filter.value)"
      :class="['filter', { active: selected === filter.value }]"
      >{{ filter.label }}</span
    >
  </div>
</template>

<style scoped>
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
