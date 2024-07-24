<template>
  <div class="album_gallery">
    <album-carousel-mobile 
      v-if="isMobileView" 
      :albums="albums" 
      :selectedFilter="selectedFilter"
      @update-album-title="updateAlbumTitle"
    ></album-carousel-mobile>
    <album-grid 
      v-else 
      :albums="albums" 
      :selectedFilter="selectedFilter"
      @update-album-title="updateAlbumTitle"
    ></album-grid>
    <album-footer 
      :filters="filters" 
      :setFilter="setFilter" 
      :activeAlbumTitle="activeAlbumTitle"
      :activeAlbumImage="activeAlbumImage"
    ></album-footer>
  </div>
</template>

<script>
import { defineComponent, ref, onMounted, onUnmounted } from 'vue';
import FilterBar from '@/components/FilterBar.vue';
import AlbumCarouselMobile from '@/components/AlbumCarouselMobile.vue';
import AlbumGrid from '@/components/AlbumGrid.vue';
import AlbumFooter from '@/components/AlbumFooter.vue';
import { albums } from '@/data/albums';

export default defineComponent({
  components: { FilterBar, AlbumCarouselMobile, AlbumGrid, AlbumFooter },
  setup() {
    const isMobileView = ref(window.innerWidth < 768);
    const selectedFilter = ref('');
    const filters = ref([
      'typeOfWork_soundEngineer',
      'typeOfWork_production',
      'typeOfWork_writing'
    ]);
    const activeAlbumTitle = ref('');
    const activeAlbumImage = ref('');

    const setFilter = filter => {
      selectedFilter.value = filter;
    };

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
      selectedFilter,
      filters,
      setFilter,
      albums,
      activeAlbumTitle,
      activeAlbumImage,
      updateAlbumTitle
    };
  }
});
</script>

<style scoped>
.album_gallery {
  position: fixed;
  top: 0;
  width: 100vw;
  height: calc(100dvh - 63px);
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
