<template>
  <div class="album-grid">
    <div
      v-for="(album, index) in filteredAlbums"
      :key="index"
      class="grid-item"
      @mouseover="updateAlbumTitle(album.title, album.image)"
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
    selectedFilter: {
      type: String,
      default: ''
    }
  },
  emits: ['update-album-title'],
  setup(props, { emit }) {
    const filteredAlbums = computed(() => {
      if (!props.selectedFilter) return props.albums;
      return props.albums.filter(album =>
        album.filters.includes(props.selectedFilter)
      );
    });

    const updateAlbumTitle = (title, image) => {
      emit('update-album-title', { title, image });
    };

    return {
      filteredAlbums,
      updateAlbumTitle
    };
  }
});
</script>

<style scoped>
.album-grid {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  gap: 20px;
  padding: 2rem;
}

.grid-item {
  position: relative;
  cursor: pointer;
}

.album-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 2px;
}
</style>
