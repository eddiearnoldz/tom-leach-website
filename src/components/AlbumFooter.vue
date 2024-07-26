<template>
  <div class="album-footer">
    <div v-if="activeAlbumTitle" class="album-title" :style="backgroundStyle">
      {{ activeAlbumTitle }} 
    </div>
    <div v-if="activeAlbumContributions.length > 0" class="album--contributions" :style="backgroundStyle">
       {{ activeAlbumContributions.join(' - ') }}
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
    },
    activeAlbumContributions: {
      type: Array,
      default: () => []
    }
  },
  computed: {
    backgroundStyle() {
      if (window.innerWidth >= 768) {
        return {
          backgroundImage: `linear-gradient(to bottom, rgba(255, 255, 255, 0.5), rgba(255, 255, 255, 0.2)), url(${this.activeAlbumImage})`,
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

.album-title,
.album--contributions {
  width: 100%;
  margin-right: auto;
  text-align: center;
  font-size: 24px; /* Adjust as needed */
  font-weight: bold; /* Adjust as needed */
  text-align: left;
  line-height: 1.2;
}

.album--contributions {
  font-size: 16px;
  text-align: right;
}



@media screen and (min-width: 768px) {
  .album-title,
  .album--contributions {
    font-size: 30px;
    width: 20vw;
    margin-right: auto;
  }
  .album--contributions {
    margin-bottom: 10vh;
    font-size: 20px;
  }

  .album-footer {
    padding: 1rem 2rem;
    padding-right: 0;
    width: 25vw;
  }
}

@media screen and (min-width: 1024px) {
  .album-title {
    font-size: 40px;
  }

  .album--contributions {
    font-size: 30;
  }
}
</style>
