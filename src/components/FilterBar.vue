<template>
  <div class="filter-bar">
    <div v-if="!isMobile || isOpen" class="filters">
      <div class="filter-group" v-for="(group, index) in groupedFilters" :key="index">
        <h3>{{ group.name.replace("-", " ") }}</h3>
        <div class="filter-options">
          <button
            v-for="filter in group.filters"
            :key="filter"
            @click="toggleFilter(filter)"
            :class="{ active: isSelected(filter) }"
          >
            {{ filter.split("_")[1].replace("-", " ") }}
          </button>
        </div>
      </div>
    </div>
    <h2 v-if="isMobile" @click="toggleFilters">FILTER<span>(<span v-if="!isOpen">+</span><span v-if="isOpen">-</span>)</span></h2>
    <button v-if="selectedFilters.length > 0" @click="clearFilters" class="clear-filters">clear ✕</button>
  </div>
</template>

<script>
import { defineComponent, ref, computed } from 'vue';

export default defineComponent({
  props: {
    filters: {
      type: Array,
      required: true
    },
    selectedFilters: {
      type: Array,
      default: () => []
    }
  },
  setup(props) {
    const isMobile = ref(window.innerWidth < 768);
    const isOpen = ref(false);

    const updateView = () => {
      isMobile.value = window.innerWidth < 768;
    };

    const toggleFilters = () => {
      if (isMobile.value) {
        isOpen.value = !isOpen.value;
      }
    };

    window.addEventListener('resize', updateView);

    const groupedFilters = computed(() => {
      const groups = {};

      props.filters.forEach(filter => {
        const [group, name] = filter.split("_");
        if (!groups[group]) {
          groups[group] = [];
        }
        groups[group].push(filter);
      });

      return Object.keys(groups).map(key => ({
        name: key.replace("-", " ").toUpperCase(),
        filters: groups[key]
      }));
    });

    return {
      isMobile,
      isOpen,
      groupedFilters,
      toggleFilters
    };
  },
  methods: {
    toggleFilter(filter) {
      this.$emit('filter-selected', filter);
    },
    isSelected(filter) {
      return this.selectedFilters.includes(filter);
    },
    clearFilters() {
      this.$emit('clear-filters');
    }
  }
});
</script>

<style scoped>
.filter-bar {
  display: flex;
  flex-direction: column;
  justify-content: center;
  overflow-x: scroll;
  z-index: 1;
  width: 100vw;
}

.filter-bar h2 {
  font-size: 1rem;
  cursor: pointer;
}

.filters {
  display: flex;
  flex-direction: row;
  gap: 10px;
}

.filter-group {
  display: flex;
  flex-direction: column;
  padding: 0;
}

.filter-group h3 {
  font-weight: bold;
  margin: 5px 0;
  font-size: 1rem;
}

.filter-options {
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  max-height: calc(1.2rem * 5);
  align-items: flex-start;
}

.filter-bar button {
  padding: 3px;
  background-color: transparent;
  border: none;
  cursor: pointer;
  color: white;
  font-size: 0.8rem;
  margin: 0px;
}

.filter-bar button.active {
  color: #FEC600;
}

.clear-filters {
  position: absolute;
  bottom: 0px;
  right: 20px;
  background-color: transparent;
  border: none;
  color: white;
  font-size: 1rem;
  cursor: pointer;
}

@media (min-width: 768px) {
  .filters {
    display: flex !important;
  }
}
</style>
