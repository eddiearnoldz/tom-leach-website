<template>
  <div class="carousel-container" ref="carouselContainer" @scroll="onScroll">
    <div
      v-for="(album, index) in filteredAlbums"
      :key="index"
      :class="['slide', { 'active-slide': activeIndex === index }]"
      :style="getSlideStyle(index)"
    >
      <img :src="album.image" :alt="album.title" class="album-image" />
    </div>
  </div>
</template>

<script>
import { defineComponent, ref, computed, onMounted, nextTick, watch, onBeforeUnmount } from 'vue';

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
    const activeIndex = ref(0);
    const carouselContainer = ref(null);

    const filteredAlbums = computed(() => {
      if (props.selectedFilters.length === 0) return props.albums;
      return props.albums.filter(album => {
        return props.selectedFilters.every(filter => album.filters.includes(filter));
      });
    });

    const getSlideStyle = (index) => {
      return {
        transform: index === activeIndex.value ? 'scale(1)' : 'scale(0.8)',
        transition: 'transform 0.3s'
      };
    };

    const onScroll = () => {
      const container = carouselContainer.value;
      if (!container) return;

      const slideHeight = window.innerWidth - 30; // 100vw - 3rem (1rem = 16px)
      const thresholdY = container.scrollTop + slideHeight / 2; // Calculate current center position based on scrollTop

      let closestIndex = 0;
      let closestDistance = Infinity;

      const slides = container.children;
      for (let i = 0; i < slides.length; i++) {
        const slideTopY = i * slideHeight + slideHeight / 2; // Middle of each slide
        const distance = Math.abs(thresholdY - slideTopY);

        if (distance < closestDistance) {
          closestDistance = distance;
          closestIndex = i;
        }
      }

        activeIndex.value = closestIndex;
        emit('update-album-title', {
          title: filteredAlbums.value[closestIndex].title,
          image: filteredAlbums.value[closestIndex].image,
          contributions: filteredAlbums.value[closestIndex].filters
            .filter(filter => filter.includes('contribution'))
            .map(filter => filter.replace('contribution_', '').replace("-", " ")),
        });
    };

    onMounted(() => {
      const container = carouselContainer.value;
      if (container) {
        container.addEventListener('scroll', onScroll);
      }

      nextTick(() => {
        onScroll(); // Initial call to set the first active slide
      });
    });

    onBeforeUnmount(() => {
      const container = carouselContainer.value;
      if (container) {
        container.removeEventListener('scroll', onScroll);
      }
    });

    watch(activeIndex, (newIndex) => {
      emit('update-album-title', {
        title: filteredAlbums.value[newIndex].title,
        image: filteredAlbums.value[newIndex].image,
        contributions: filteredAlbums.value[newIndex].filters
          .filter(filter => filter.includes('contribution'))
          .map(filter => filter.replace('contribution_', '').replace("-", " ")),
      });
    });

    return {
      activeIndex,
      filteredAlbums,
      getSlideStyle,
      carouselContainer
    };
  }
});
</script>

<style scoped>
.carousel-container {
  height: 100dvh;
  overflow-y: scroll;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 30vh 1.5rem 30vh;
}

.slide {
  width: calc(100vw - 3rem);
  height: calc(100vw - 3rem); /* Height is equal to the width */
  margin: 5px 0;
  transition: transform 0.3s;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: relative;
  scroll-snap-align: start;
}

.active-slide {
  transform: scale(1);
}

.album-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 2px;
}
</style>
