<template>
  <div class="filter-bar">
    <div v-if="!isMobile || isOpen" class="filters">
      <div class="filter-group" v-for="(group, index) in groupedFilters" :key="index">
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
      <h3>{{ group.name.replace("-", " ") }}</h3>
      </div>
    </div>
    <h2  @click="toggleFilters">FILTERS<span v-if="isMobile">(<span v-if="!isOpen">+</span><span v-if="isOpen">-</span>)</span></h2>
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
  width: 100%;
}

.filter-bar h2 {
  font-size: 0.8rem;
  cursor: pointer;
  font-weight: bold;
}

.filters {
  display: flex;
  flex-direction: row;
  gap: 20px;
}

.filter-group {
  display: flex;
  flex-direction: column;
  padding: 0;
  width: max-content;
  justify-content: flex-end;
}

.filter-group h3 {
  font-weight: bold;
  font-size: 0.8rem;
  width: 100%;
}

.filter-options {
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  align-items: flex-start;

}

.filter-bar button {
  padding: 1px;
  background-color: transparent;
  border: none;
  cursor: pointer;
  color: white;
  font-size: 0.8rem;
  margin: 0px;
}

.filter-bar button.active,
.filter-bar button.active:hover  {
  color: #FEC600;
}

.clear-filters {
  position: absolute;
  bottom: 0;
  right: 0;
  background-color: transparent;
  border: none;
  color: white;
  font-size: 1rem;
  cursor: pointer;
}

@media (min-width: 768px) {
  .filters {
    display: flex !important;
    gap:clamp(10px, 1vw, 20px)
  }

  .filter-bar button,
  .filter-group h3,
  .filter-bar h2  {
    font-size: clamp(0.6rem, 1.1vw, 1.2rem);
  }

  .clear-filters {
    right: 20px;
  }

  .filter-bar button:hover {
    color: #fe5d00;
  }

}
</style>
