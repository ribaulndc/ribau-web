<template>
  <div class="product-card">
    <div class="image-container">
      <!-- Image Carousel -->
      <div class="carousel">
        <img 
          :src="currentImage" 
          :alt="`${product.name} - Image ${currentImageIndex + 1}`"
          @error="handleImageError"
          class="product-image"
        >
        
        <!-- Navigation Arrows (only show if multiple images) -->
        <button 
          v-if="hasMultipleImages"
          class="carousel-btn prev"
          @click.stop="prevImage"
          aria-label="Previous image"
        >
          ‹
        </button>
        <button 
          v-if="hasMultipleImages"
          class="carousel-btn next"
          @click.stop="nextImage"
          aria-label="Next image"
        >
          ›
        </button>

        <!-- Image Dots Indicator -->
        <div v-if="hasMultipleImages" class="carousel-dots">
          <span 
            v-for="(img, index) in availableImages" 
            :key="index"
            :class="['dot', { active: index === currentImageIndex }]"
            @click.stop="goToImage(index)"
          ></span>
        </div>
      </div>

      <!-- Badges -->
      <span v-if="product.featured" class="badge featured">⭐ Featured</span>
      <span v-if="!product.inStock" class="badge out-of-stock">Sold Out</span>
    </div>
    
    <div class="product-info">
      <h3>{{ product.name }}</h3>
      <p class="category">{{ product.category }}</p>
      <p class="description">{{ product.description }}</p>
      <div class="product-footer">
        <span class="price">€{{ product.price.toFixed(2) }}</span>
        <button 
          class="contact-btn"
          :disabled="!product.inStock"
          @click="$emit('contact', product)"
        >
          {{ product.inStock ? 'Richiedi Info' : 'Non Disponibile' }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductCard',
  props: {
    product: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      currentImageIndex: 0,
      availableImages: [],
      fallbackImage: '/images/lobo_fallback.jpeg'
    };
  },
  computed: {
    currentImage() {
      return this.availableImages[this.currentImageIndex] || this.fallbackImage;
    },
    hasMultipleImages() {
      return this.availableImages.length > 1;
    }
  },
  mounted() {
    this.loadAvailableImages();
  },
  methods: {
    async loadAvailableImages() {
      const images = [];
      
      // Helper function to check if image exists
      const checkImage = (src) => {
        return new Promise((resolve) => {
          const img = new Image();
          img.onload = () => resolve(true);
          img.onerror = () => resolve(false);
          img.src = src;
        });
      };

      // Check single image format (id.jpg)
      const singleImg = `/images/products/${this.product.id}.jpg`;
      if (await checkImage(singleImg)) {
        images.push(singleImg);
      }
      
      // Check numbered format (id_1.jpg, id_2.jpg, id_3.jpg)
      for (let i = 1; i <= 3; i++) {
        const numberedImg = `/images/products/${this.product.id}_${i}.jpg`;
        if (await checkImage(numberedImg)) {
          images.push(numberedImg);
        }
      }

      // Set available images or fallback
      this.availableImages = images.length > 0 ? images : [this.fallbackImage];
    },
    handleImageError(event) {
      // Remove failed image from available images
      const failedSrc = event.target.src;
      const imgIndex = this.availableImages.findIndex(img => 
        failedSrc.includes(img)
      );
      
      if (imgIndex !== -1) {
        this.availableImages.splice(imgIndex, 1);
        
        // If we removed the current image, adjust index
        if (this.currentImageIndex >= this.availableImages.length) {
          this.currentImageIndex = Math.max(0, this.availableImages.length - 1);
        }
      }

      // If no images left, show fallback
      if (this.availableImages.length === 0) {
        event.target.src = this.fallbackImage;
      }
    },
    nextImage() {
      this.currentImageIndex = (this.currentImageIndex + 1) % this.availableImages.length;
    },
    prevImage() {
      this.currentImageIndex = 
        (this.currentImageIndex - 1 + this.availableImages.length) % this.availableImages.length;
    },
    goToImage(index) {
      this.currentImageIndex = index;
    }
  }
};
</script>

<style scoped>
.product-card {
  background: white;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  overflow: hidden;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  display: flex;
  flex-direction: column;
}

.product-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 4px 16px rgba(0,0,0,0.15);
}

.image-container {
  position: relative;
  width: 100%;
  height: 250px;
  background: #f8f9fa;
}

.carousel {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.product-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.carousel-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: rgba(0, 0, 0, 0.5);
  color: white;
  border: none;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  font-size: 24px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background 0.3s ease;
  z-index: 10;
}

.carousel-btn:hover {
  background: rgba(0, 0, 0, 0.7);
}

.carousel-btn.prev {
  left: 10px;
}

.carousel-btn.next {
  right: 10px;
}

.carousel-dots {
  position: absolute;
  bottom: 10px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 8px;
  z-index: 10;
}

.dot {
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.5);
  cursor: pointer;
  transition: background 0.3s ease, transform 0.3s ease;
}

.dot:hover {
  background: rgba(255, 255, 255, 0.8);
  transform: scale(1.2);
}

.dot.active {
  background: white;
  transform: scale(1.3);
}

.badge {
  position: absolute;
  top: 10px;
  right: 10px;
  padding: 5px 12px;
  border-radius: 15px;
  font-size: 0.85rem;
  font-weight: bold;
  z-index: 10;
}

.badge.featured {
  background: #f39c12;
  color: white;
}

.badge.out-of-stock {
  background: #e74c3c;
  color: white;
}

.product-info {
  padding: 20px;
  display: flex;
  flex-direction: column;
  flex-grow: 1;
}

.product-info h3 {
  font-size: 1.3rem;
  color: #2c3e50;
  margin-bottom: 5px;
}

.category {
  color: #3498db;
  font-size: 0.9rem;
  font-weight: 600;
  margin-bottom: 10px;
}

.description {
  color: #7f8c8d;
  font-size: 0.95rem;
  line-height: 1.5;
  margin-bottom: 15px;
  min-height: 60px;
}

.product-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: auto;
}

.price {
  font-size: 1.5rem;
  color: #27ae60;
  font-weight: bold;
}

.contact-btn {
  padding: 10px 20px;
  background: #3498db;
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-size: 1rem;
  transition: background 0.3s ease;
}

.contact-btn:hover:not(:disabled) {
  background: #2980b9;
}

.contact-btn:disabled {
  background: #95a5a6;
  cursor: not-allowed;
}
</style>
