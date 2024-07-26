<template>
  <div class="album-grid">
    <div
      v-for="(album, index) in filteredAlbums"
      :key="index"
      class="grid-item"
      @mouseover="handleMouseOver(album)"
      @mouseleave="handleMouseLeave"
      @click="handleClick(album)"
    >
      <img :src="album.image" :alt="album.title" class="album-image" />
    </div>
    <video-modal
      :isVisible="isModalVisible"
      :videoId="currentVideoId"
      :videoTitle="currentVideoTitle"
      @close="isModalVisible = false"
    />
  </div>
</template>

<script>
import { defineComponent, computed, ref } from 'vue';
import VideoModal from '@/components/VideoModal.vue';

export default defineComponent({
  components: {
    VideoModal
  },
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
    const isModalVisible = ref(false);
    const currentVideoId = ref('');
    const currentVideoTitle = ref('');

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

    const handleClick = (album) => {
      if (album.videoUrl) {
        // Extract the video ID from the URL
        const videoId = album.videoUrl.split('v=')[1];
        currentVideoId.value = videoId;
        currentVideoTitle.value = album.title;
        isModalVisible.value = true;
        document.body.style.overflow = 'hidden'; // Stop scrolling
      }
    };

    return {
      filteredAlbums,
      handleMouseOver,
      handleMouseLeave,
      handleClick,
      isModalVisible,
      currentVideoId,
      currentVideoTitle
    };
  },
  watch: {
    isModalVisible(newValue) {
      if (!newValue) {
        document.body.style.overflow = ''; // Enable scrolling
      }
    }
  }
});
</script>

<style scoped>
.album-grid {
  display: grid;
  grid-template-columns: repeat(5, calc(20% - 10px));
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
