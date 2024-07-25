<template>
  <div class="album_gallery">
    <album-carousel-mobile 
      v-if="isMobileView" 
      :albums="filteredAlbums" 
      :selectedFilters="selectedFilters"
      @update-album-title="updateAlbumTitle"
    ></album-carousel-mobile>
    <album-grid 
      v-else 
      :albums="filteredAlbums" 
      :selectedFilters="selectedFilters"
      @update-album-title="updateAlbumTitle"
    ></album-grid>
    <album-footer 
      :filters="filters" 
      :toggleFilter="toggleFilter" 
      @clear-filters="clearFilters"
      :activeAlbumTitle="activeAlbumTitle"
      :activeAlbumImage="activeAlbumImage"
      :selectedFilters="selectedFilters"
    ></album-footer>
  </div>
</template>

<script>
import { defineComponent, ref, computed, onMounted, onUnmounted } from 'vue';
import AlbumCarouselMobile from '@/components/AlbumCarouselMobile.vue';
import AlbumGrid from '@/components/AlbumGrid.vue';
import AlbumFooter from '@/components/AlbumFooter.vue';
import { albums } from '@/data/albums';

export default defineComponent({
  components: { AlbumCarouselMobile, AlbumGrid, AlbumFooter },
  setup() {
    const isMobileView = ref(window.innerWidth < 768);
    const selectedFilters = ref([]);
    const filters = ref([
      'contribution_sound-engineer',
      'contribution_production',
      'contribution_writing',
      'year_2020',
      'year_2021',
      'year_2022',
      'year_2023',
      'year_2024',
      'genre_rock',
      'genre_indie',
      'genre_alt',
      'genre_trap',
      'genre_rap'
    ]);
    const activeAlbumTitle = ref('');
    const activeAlbumImage = ref('');

    const toggleFilter = filter => {
      const index = selectedFilters.value.indexOf(filter);
      if (index === -1) {
        selectedFilters.value.push(filter);
      } else {
        selectedFilters.value.splice(index, 1);
      }
    };

    const clearFilters = () => {
      selectedFilters.value = [];
    };

    const filteredAlbums = computed(() => {
      if (selectedFilters.value.length === 0) return albums;
      return albums.filter(album =>
        selectedFilters.value.every(filter => album.filters.includes(filter))
      );
    });

    const updateView = () => {
      isMobileView.value = window.innerWidth < 768;
    };

    const updateAlbumTitle = ({ title, image }) => {
      activeAlbumTitle.value = title;
      activeAlbumImage.value = image;
    };

    onMounted(() => {
      window.addEventListener('resize', updateView);
    });

    onUnmounted(() => {
      window.removeEventListener('resize', updateView);
    });

    return {
      isMobileView,
      selectedFilters,
      filters,
      albums,
      activeAlbumTitle,
      activeAlbumImage,
      updateAlbumTitle,
      toggleFilter,
      clearFilters,
      filteredAlbums
    };
  }
});
</script>

<style scoped>
.album_gallery {
  position: fixed;
  top: 0;
  width: 100vw;
  height: 100dvh;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

@media screen and (min-width:768px) {
  .album_gallery {
    top: 63px;
  }
}
</style>
