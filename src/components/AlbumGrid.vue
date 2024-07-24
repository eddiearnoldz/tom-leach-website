<!-- AlbumGrid.vue -->
<template>
  <div class="album-grid">
    <div
      v-for="(album, index) in filteredAlbums"
      :key="index"
      class="album-tile"
    >
      <img :src="album.image" :alt="album.title" />
      <div class="album-title">{{ album.title }}</div>
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
  computed: {
    filteredAlbums() {
      if (!this.selectedFilter) return this.albums;
      return this.albums.filter(album =>
        album.filters.includes(this.selectedFilter)
      );
    }
  }
});
</script>

<style scoped>
.album-grid {
  display: grid;
  grid-template-columns: repeat(6, 10vw);
  grid-template-rows: repeat(3, 10vw);
  gap: 20px;
  padding: 40px;
}

.album-tile {
  position: relative;
  width: 100%;
  height: 100%;
}

.album-tile img {
  width: 100%;
  height: 100%;
}

.album-title {
  position: absolute;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.7);
  color: white;
  width: 100%;
  text-align: center;
}
</style>
