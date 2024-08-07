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
      :activeAlbumContributions="activeAlbumContributions"
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
      'contribution_recording-engineer',
      'contribution_production',
      'contribution_writer',
      'contribution_producer',
      'contribution_mixer',
      'contribution_mastering',
      'year_2017',
      'year_2019',
      'year_2020',
      'year_2021',
      'year_2022',
      'year_2023',
      'year_2024',
      'genre_rock',
      'genre_indie',
      'genre_alt',
      'genre_afrobeat',
      'genre_rap',
      'genre_pop',
      'genre_electronic'
    ]);
    const activeAlbumTitle = ref('');
    const activeAlbumImage = ref('');
    const activeAlbumContributions = ref([]);

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

    const updateAlbumTitle = ({ title, image, contributions }) => {
      activeAlbumTitle.value = title;
      activeAlbumImage.value = image;
      activeAlbumContributions.value = contributions;
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
      activeAlbumContributions,
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
  position: absolute;
  top: 0;
  width: 100vw;
  height: max-content;
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
