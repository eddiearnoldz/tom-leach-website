<template>
  <div class="album-footer">
    <div class="album-title" :style="backgroundStyle">
      {{ activeAlbumTitle }}
    </div>
    <filter-bar :filters="filters" @filter-selected="setFilter"></filter-bar>
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
    setFilter: {
      type: Function,
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
          backgroundImage: `url(${this.activeAlbumImage})`,
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
  padding: 10px 0;
  background-image: linear-gradient(to top, rgba(0, 0, 0, 0.8), rgba(0, 0, 0, 0) 100%);
}

.album-title {
  width: 100%;
  text-align: center;
  padding: 0 16px;
  font-size: 24px; /* Adjust as needed */
  font-weight: bold; /* Adjust as needed */
  text-align: left;
}

.filter-bar {
  margin-top: 10px;
}

@media screen and (min-width: 768px) {
  .album-title {
    font-size: 40px; /* Adjust as needed */
  }
}
</style>
