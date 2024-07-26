<template>
  <div class="album-grid">
    <div
      v-for="(album, index) in filteredAlbums"
      :key="index"
      class="grid-item"
      @mouseover="handleMouseOver(album)"
      @mouseleave="handleMouseLeave"
    >
      <img :src="album.image" :alt="album.title" class="album-image" />
    </div>
  </div>
</template>

<script>
import { defineComponent, computed } from 'vue';

export default defineComponent({
  props: {
    albums: {
      type: Array,
      required: true
    },
    selectedFilters: {
      type: Array,
      default: () => []
    }
  },
  emits: ['update-album-title'],
  setup(props, { emit }) {
    const filteredAlbums = computed(() => {
      if (props.selectedFilters.length === 0) return props.albums;
      return props.albums.filter(album => {
        return props.selectedFilters.every(filter => album.filters.includes(filter));
      });
    });

    const updateAlbumTitle = (title, image, contributions) => {
      emit('update-album-title', { title, image, contributions });
    };

    const handleMouseOver = (album) => {
      try {
        const contributions = album.filters.filter(filter => filter.includes('contribution')).map(filter => filter.replace('contribution_', '').replace("-", " "));
        updateAlbumTitle(album.title, album.image, contributions);
      } catch (error) {
        console.error('Error in handleMouseOver:', error);
      }
    };

    const handleMouseLeave = () => {
      try {
        updateAlbumTitle('', '', []);
      } catch (error) {
        console.error('Error in handleMouseLeave:', error);
      }
    };

    return {
      filteredAlbums,
      handleMouseOver,
      handleMouseLeave
    };
  }
});
</script>

<style scoped>
.album-grid {
  display: grid;
  grid-template-columns: repeat(5, calc(20% - 9px));
  gap: 10px;
  padding: 2rem;
  padding-left: 0;
  overflow: scroll;
  height: 100%;
  width: 75vw;
  margin-left: auto;
}

.grid-item {
  position: relative;
  cursor: pointer;
  overflow: hidden;
}

.album-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 2px;
  aspect-ratio: 1;
  transform: scale(1);
  transition: transform 0.3s, margin 0.3s;
}

.album-image:hover {
  transform: scale(1.2);
}
</style>
