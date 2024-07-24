<template>
  <div class="album_gallery">
    <filter-bar
      :filters="filters"
      @filter-selected="setFilter"
    ></filter-bar>
    <album-carousel-mobile v-if="isMobileView" :albums="albums" :selectedFilter="selectedFilter"></album-carousel-mobile>
    <album-grid v-else :albums="albums" :selectedFilter="selectedFilter"></album-grid>
  </div>
</template>

<script>
import { defineComponent, ref, onMounted, onUnmounted } from 'vue';
import FilterBar from '@/components/FilterBar.vue';
import AlbumCarouselMobile from '@/components/AlbumCarouselMobile.vue';
import AlbumGrid from '@/components/AlbumGrid.vue';
import { albums } from '@/data/albums';

export default defineComponent({
  components: { FilterBar, AlbumCarouselMobile, AlbumGrid },
  setup() {
    const isMobileView = ref(window.innerWidth < 768);
    const selectedFilter = ref('');
    const filters = ref([
      'typeOfWork_soundEngineer',
      'typeOfWork_production',
      'typeOfWork_writing'
    ]);

    const setFilter = filter => {
      selectedFilter.value = filter;
    };

    const updateView = () => {
      isMobileView.value = window.innerWidth < 768;
    };

    onMounted(() => {
      window.addEventListener('resize', updateView);
    });

    onUnmounted(() => {
      window.removeEventListener('resize', updateView);
    });

    return {
      isMobileView,
      selectedFilter,
      filters,
      setFilter,
      albums
    };
  }
});
</script>

<style scoped>
.album_gallery {
  position: fixed;
  top: 63px;
  width: 100vw;
  height: calc(100dvh - 63px);
}
</style>
