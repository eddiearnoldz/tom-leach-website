<template>
  <div class="carousel-container" ref="carouselContainer" @scroll="onScroll">
    <div
      v-for="(album, index) in filteredAlbums"
      :key="index"
      :class="['slide', { 'active-slide': activeIndex === index }]"
      :style="getSlideStyle(index)"
    >
      <img :src="album.image" :alt="album.title" class="album-image" />
      <div v-if="activeIndex === index" class="album-title">{{ album.title }}</div>
    </div>
  </div>
</template>

<script>
import { defineComponent, ref, computed, onMounted, nextTick } from 'vue';

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
  setup(props) {
    const activeIndex = ref(0);
    const carouselContainer = ref(null);

    const filteredAlbums = computed(() => {
      if (!props.selectedFilter) return props.albums;
      return props.albums.filter(album =>
        album.filters.includes(props.selectedFilter)
      );
    });

    const getSlideStyle = (index) => {
      const container = carouselContainer.value;
      if (!container) return {};

      const slide = container.children[index];
      const slideRect = slide.getBoundingClientRect();
      const slideMiddleY = slideRect.top + slideRect.height / 2;
      const thresholdY = window.innerHeight * 0.5; // 50vh from the top

      let scale;
      if (index === activeIndex.value) {
        scale = 1;
      } else if (slideMiddleY > thresholdY) {
        const distanceToThreshold = slideMiddleY - thresholdY;
        const maxDistance = window.innerHeight - thresholdY;
        const scaleFactor = Math.max(0.3, 1 - (distanceToThreshold / maxDistance));
        scale = scaleFactor;
      } else {
        scale = 1;
      }

      return {
        transform: `scale(${scale})`,
      };
    };

    const onScroll = () => {
      const container = carouselContainer.value;
      const thresholdY = window.innerHeight * 0.5; // 50vh from the top

      let closestIndex = 0;
      let closestDistance = Infinity;

      const slides = container.children;
      for (let i = 0; i < slides.length; i++) {
        const slide = slides[i];
        const slideRect = slide.getBoundingClientRect();
        const slideMiddleY = slideRect.top + slideRect.height / 2;
        const distance = Math.abs(thresholdY - slideMiddleY);

        if (distance < closestDistance) {
          closestDistance = distance;
          closestIndex = i;
        }
      }

      activeIndex.value = closestIndex;
    };

    const initializeScaling = () => {

      const container = carouselContainer.value;
      const slides = container.children;
      for (let i = 0; i < slides.length; i++) {
        getSlideStyle(i);
      }
    };

    onMounted(() => {
      const container = carouselContainer.value;
      container.addEventListener('scroll', onScroll);
      nextTick(() => {
        initializeScaling();
        onScroll(); 
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
  height: 100vh;
  overflow-y: scroll;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20vh 0.5rem 50vh;
}

.slide {
  width: 100%;
  height: 25vh;
  margin: 5px 0;
  transition: transform 0.3s;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: relative;
}

.album-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 2px;
}

.album-title {
  position: absolute;
  bottom: 10px;
  background-color: rgba(0, 0, 0, 0.7);
  color: white;
  padding: 5px 10px;
  border-radius: 5px;
}
</style>
