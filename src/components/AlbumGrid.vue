<template>
  <div class="album-grid">
    <div
      v-for="(album, index) in filteredAlbums"
      :key="index"
      class="grid-item"
      @mouseover="updateAlbumTitle(album.title, album.image)"
      @mouseleave="clearAlbumTitle"
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

    const updateAlbumTitle = (title, image) => {
      emit('update-album-title', { title, image });
    };
    const clearAlbumTitle = () => {
      emit('update-album-title', { title: '', image: '' });
    };

    return {
      filteredAlbums,
      updateAlbumTitle,
      clearAlbumTitle
    };
  }
});
</script>

<style scoped>
.album-grid {
  display: grid;
  grid-template-columns: repeat(8, calc(12.5% - 10px));
  grid-template-rows: repeat(3, 1fr);
  gap: 10px;
  padding: 2rem;
  overflow: scroll;
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
