<!-- src/components/VideoModal.vue -->
<template>
  <div v-if="isVisible" class="modal-overlay" @click="closeModal">
    <div class="modal-content" @click.stop>
      <button class="close-button" @click="closeModal">✕</button>
      <LiteYouTubeEmbed
        :id=videoId
        ref="iframe"
        :title=videoTitle
        params="autoplay=1&controls=0"
        :webp="true"
      />
      <span class="popup-album-title" >{{ videoTitle }}</span>
    </div>
  </div>
</template>

<script>
import LiteYouTubeEmbed from 'vue-lite-youtube-embed'
import 'vue-lite-youtube-embed/style.css'

export default {
  name: 'VideoModal',
  components: {
    LiteYouTubeEmbed
  },
  props: {
    isVisible: {
      type: Boolean,
      default: false
    },
    videoId: {
      type: String,
      default: ''
    },
    videoTitle: {
      type: String,
      default: ''
    }
  },
  methods: {
    closeModal() {
      this.$emit('close');
    }
  }
};
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.9);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-content {
  position: relative;
  width: 80%;
  max-width: 1000px;
  background-color: black;
  padding: 1rem;
  border-radius: 10px;
}

.close-button {
  position: absolute;
  top: -40px;
  right: 10px;
  background: transparent;
  border: none;
  color: white;
  font-size: 2.5rem;
  cursor: pointer;
  z-index: 1;
}

.popup-album-title {
  width: 100%;
  margin-right: auto;
  text-align: center;
  font-size: 24px; 
  font-weight: bold; 
  text-align: left;
  line-height: 1.2;
  position: absolute;
  top: -30px;
  left: 10px;
}
</style>
