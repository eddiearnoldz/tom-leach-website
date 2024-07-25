<template>
  <div class="album-footer">
    <div class="album-title" :style="backgroundStyle">
      {{ activeAlbumTitle }}
    </div>
    <filter-bar 
      :filters="filters" 
      @filter-selected="toggleFilter"
      :selectedFilters="selectedFilters"
       @clear-filters="$emit('clear-filters')"
    ></filter-bar>
  </div>
</template>

<script>
import FilterBar from '@/components/FilterBar.vue';

export default {
  components: { FilterBar },
  props: {
    filters: {
      type: Array,
      required: true
    },
    toggleFilter: {
      type: Function,
      required: true
    },
    selectedFilters: {
      type: Array,
      required: true
    },
    activeAlbumTitle: {
      type: String,
      default: ''
    },
    activeAlbumImage: {
      type: String,
      default: ''
    }
  },
  computed: {
    backgroundStyle() {
      if (window.innerWidth >= 768) {
        return {
          backgroundImage: `linear-gradient(to bottom, rgba(255, 255, 255, 0.2), rgba(255, 255, 255, 0.2)), url(${this.activeAlbumImage})`,
          backgroundSize: 'cover',
          backgroundRepeat: 'no-repeat',
          backgroundPosition: 'center',
          color: 'transparent',
          backgroundClip: 'text',
          WebkitBackgroundClip: 'text'
        };
      }
      return {};
    }
  }
};
</script>

<style scoped>
.album-footer {
  position: fixed;
  bottom: 0;
  width: 100%;
  color: white;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 10px 1rem;
  background-image: linear-gradient(to top, rgba(0, 0, 0, 1), rgba(0, 0, 0, 0) 100%);
}

.album-title {
  width: 100%;
  text-align: center;
  font-size: 24px; /* Adjust as needed */
  font-weight: bold; /* Adjust as needed */
  text-align: left;
}

@media screen and (min-width: 768px) {
  .album-title {
    font-size: 40px; /* Adjust as needed */
  }
}
</style>
