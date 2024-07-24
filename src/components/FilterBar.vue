<!-- FilterBar.vue -->
<template>
  <div class="filter-bar">
    <h2>FILTERS</h2>
    <div class="filters">
      <button
        v-for="filter in filters"
        :key="filter"
        @click="$emit('filter-selected', filter)"
      >
        {{ filter }}
      </button>
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  props: {
    filters: {
      type: Array,
      required: true
    }
  }
});
</script>

<style scoped>

.filter-bar {
  display: flex;
  flex-direction: column;
  gap: 10px;
  justify-content: center;
  position: absolute;
  bottom: 0px;
  overflow-x: hidden;
  z-index: 101020102102;
}

.filters {
  display: flex;
  overflow-x: scroll;
}

.filter-bar button {
  padding: 10px;
  background-color: transparent;
  border: none;
  cursor: pointer;
  color: white;
}
</style>
