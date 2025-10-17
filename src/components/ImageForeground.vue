<template>
  <div v-if="imageUrl" class="modal-overlay" @click="$emit('close')">
    <div class="modal-content" @click.stop>
      <img :src="imageUrl" alt="Enlarged product view" class="enlarged-image">
      <button class="close-btn" @click="$emit('close')" aria-label="Close image view">
        &times;
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ImageModal',
  props: {
    imageUrl: {
      type: String,
      default: null
    }
  },
  emits: ['close']
};
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.85); /* Darker for better focus */
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 2000; /* Higher than other elements */
  cursor: pointer;
}

.modal-content {
  position: relative;
  max-width: 90vw;
  max-height: 90vh;
}

.enlarged-image {
  display: block;
  max-width: 100%;
  max-height: 90vh; /* Ensure it fits vertically */
  border-radius: 8px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.5);
}

.close-btn {
  position: absolute;
  top: -15px;
  right: -15px;
  width: 40px;
  height: 40px;
  background: white;
  color: #333;
  border: none;
  border-radius: 50%;
  font-size: 28px;
  line-height: 40px;
  text-align: center;
  cursor: pointer;
  box-shadow: 0 2px 10px rgba(0,0,0,0.3);
}
</style>
