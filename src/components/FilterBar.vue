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
        {{ filter.split("_")[1] }}
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
  justify-content: center;
  overflow-x: hidden;
  z-index: 101020102102;
  width: 100vw;
}

.filter-bar h2{
  padding: 0 16px; 
  font-size: 1rem;
}

.filters {
  display: flex;
  overflow-x: scroll;
}

.filter-bar button {
  padding: 5px 16px;
  background-color: transparent;
  border: none;
  cursor: pointer;
  color: white;
  font-size: 0.8rem;
}
</style>
