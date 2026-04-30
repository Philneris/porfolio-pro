<template>
  <section id="services">
    <div class="container">
      <div class="services-content-wrapper">
        <div class="section-title">
          <div class="accent-line"></div>
          <h2>Mes Services</h2>
        </div>

        <div class="carousel-section">
          <!-- Category Selectors -->
          <div class="category-selectors">
             <button 
                class="filter-btn" 
                :class="{ active: activeCategory === 'Tout' }" 
                @click="setCategory('Tout')">
                Tout
             </button>
             <button 
                class="filter-btn" 
                :class="{ active: activeCategory === 'Site Vitrine' }" 
                @click="setCategory('Site Vitrine')">
                Site Vitrine
             </button>
             <button 
                class="filter-btn" 
                :class="{ active: activeCategory === 'Site E-commerce' }" 
                @click="setCategory('Site E-commerce')">
                Site E-commerce
             </button>
             <button 
                class="filter-btn" 
                :class="{ active: activeCategory === 'Application Web' }" 
                @click="setCategory('Application Web')">
                Application Web
             </button>
          </div>

          <!-- Main Carousel -->
          <div class="main-carousel">
            <button class="nav-btn prev" @click="prevImage" aria-label="Image précédente">
              <i class="fas fa-chevron-left"></i>
            </button>
            <div class="image-wrapper">
              <transition name="fade">
                <img 
                  v-if="filteredImages.length > 0"
                  :key="filteredImages[currentIndex].src"
                  :src="filteredImages[currentIndex].src" 
                  :alt="filteredImages[currentIndex].category" 
                  class="carousel-img"
                />
              </transition>
              <div class="category-label" v-if="activeCategory === 'Tout' && filteredImages.length > 0">
                {{ filteredImages[currentIndex].category }}
              </div>
            </div>
            <button class="nav-btn next" @click="nextImage" aria-label="Image suivante">
              <i class="fas fa-chevron-right"></i>
            </button>
            
            <!-- Indicators -->
            <div class="carousel-indicators" v-if="filteredImages.length > 1">
              <span 
                v-for="(_, i) in filteredImages" 
                :key="i" 
                class="dot"
                :class="{ active: currentIndex === i }"
                @click="setCurrentIndex(i)"
              ></span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

const allImages = [
  { src: '/site-vitrine-1.webp', category: 'Site Vitrine' },
  { src: '/site-vitrine-2.webp', category: 'Site Vitrine' },
  { src: '/site-vitrine-3.png', category: 'Site Vitrine' },
  { src: '/site-vitrine-4.png', category: 'Site Vitrine' },
  { src: '/site-ecommerce-1.webp', category: 'Site E-commerce' },
  { src: '/site-ecommerce-2.png', category: 'Site E-commerce' },
  { src: '/app-web-1.jpg', category: 'Application Web' },
  { src: '/app-web-2.jpg', category: 'Application Web' },
]

const activeCategory = ref('Tout')
const currentIndex = ref(0)
let interval = null

const filteredImages = computed(() => {
  if (activeCategory.value === 'Tout') return allImages
  return allImages.filter(img => img.category === activeCategory.value)
})

const nextImage = () => {
  if (filteredImages.value.length === 0) return
  currentIndex.value = (currentIndex.value + 1) % filteredImages.value.length
  resetInterval()
}

const prevImage = () => {
  if (filteredImages.value.length === 0) return
  currentIndex.value = (currentIndex.value - 1 + filteredImages.value.length) % filteredImages.value.length
  resetInterval()
}

const setCurrentIndex = (i) => {
  currentIndex.value = i
  resetInterval()
}

const setCategory = (cat) => {
  if (activeCategory.value === cat) return
  activeCategory.value = cat
  currentIndex.value = 0
  resetInterval()
}

const startInterval = () => {
  interval = setInterval(() => {
    if (filteredImages.value.length > 0) {
      currentIndex.value = (currentIndex.value + 1) % filteredImages.value.length
    }
  }, 4500)
}

const resetInterval = () => {
  if (interval) clearInterval(interval)
  startInterval()
}

onMounted(() => {
  startInterval()
})

onUnmounted(() => {
  if (interval) clearInterval(interval)
})
</script>

<style scoped>
#services {
  overflow: visible;
  position: relative;
  padding: 8rem 0;
}

.services-content-wrapper {
  position: relative;
  padding: 8rem 4rem;
  border-radius: 40% 60% 40% 60% / 35% 35% 65% 65%;
  background: linear-gradient(135deg, rgba(240, 122, 144, 0.08) 0%, rgba(228, 75, 100, 0.12) 100%);
  z-index: 1;
  transition: var(--ease);
}

.services-content-wrapper::before {
  content: '';
  position: absolute;
  inset: -10px;
  border: 1.5px solid rgba(228, 75, 100, 0.2);
  border-radius: 55% 45% 65% 35% / 40% 60% 40% 60%;
  z-index: -1;
  pointer-events: none;
  opacity: 0.6;
}

.services-content-wrapper::after {
  content: '';
  position: absolute;
  top: -60px;
  left: 50%;
  transform: translateX(-50%);
  width: 450px;
  height: 180px;
  background: var(--bg-main);
  border-radius: 50% 50% 0 0;
  z-index: -1;
  border-top: 1.5px solid rgba(228, 75, 100, 0.15);
  box-shadow: 0 -20px 40px rgba(0, 0, 0, 0.02);
}

.carousel-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 3rem;
  position: relative;
  z-index: 2;
  margin-top: 1rem;
}

.category-selectors {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  justify-content: center;
}

.filter-btn {
  padding: 0.85rem 1.75rem;
  border-radius: 50px;
  background: var(--bg-card);
  border: 1px solid var(--border-light);
  color: var(--text-muted);
  font-weight: 700;
  cursor: pointer;
  transition: var(--ease);
  font-size: 0.95rem;
  box-shadow: 0 8px 25px rgba(0,0,0,0.03);
}

.filter-btn:hover {
  border-color: rgba(221, 45, 74, 0.3);
  color: var(--red);
  transform: translateY(-3px);
  box-shadow: 0 12px 30px rgba(0,0,0,0.05);
}

.filter-btn.active {
  background: var(--red);
  color: white;
  border-color: var(--red);
  box-shadow: 0 10px 30px rgba(221, 45, 74, 0.25);
  transform: translateY(-3px);
}

.main-carousel {
  position: relative;
  width: 100%;
  max-width: 900px;
  margin: 0 auto;
}

.image-wrapper {
  width: 100%;
  height: 500px;
  border-radius: 20px;
  overflow: hidden;
  position: relative;
  background: white;
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.08);
  border: 1px solid rgba(221, 45, 74, 0.1);
}

.carousel-img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: top center;
}

.category-label {
  position: absolute;
  top: 1.5rem;
  right: 1.5rem;
  background: rgba(255, 255, 255, 0.95);
  padding: 0.6rem 1.25rem;
  border-radius: 50px;
  font-weight: 700;
  font-size: 0.9rem;
  color: var(--dark);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
  letter-spacing: -0.01em;
  z-index: 5;
}

.nav-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 10;
  width: 54px;
  height: 54px;
  border-radius: 50%;
  border: 1px solid rgba(221, 45, 74, 0.15);
  background: white;
  color: var(--dark);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.25rem;
  transition: var(--ease);
  box-shadow: 0 8px 25px rgba(0,0,0,0.08);
}

.nav-btn.prev {
  left: -27px;
}

.nav-btn.next {
  right: -27px;
}

.nav-btn:hover {
  background: var(--red);
  color: white;
  border-color: var(--red);
  transform: translateY(-50%) scale(1.1);
  box-shadow: 0 10px 30px rgba(221, 45, 74, 0.3);
}

.carousel-indicators {
  position: absolute;
  bottom: -35px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  gap: 10px;
}

.dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: rgba(221, 45, 74, 0.2);
  cursor: pointer;
  transition: all 0.4s ease;
}

.dot.active {
  background: var(--red);
  width: 26px;
  border-radius: 4px;
}

.dot:hover:not(.active) {
  background: rgba(221, 45, 74, 0.5);
}

/* Vue transitions */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.8s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

@media (max-width: 1200px) {
  .services-content-wrapper {
    padding: 6rem 3rem;
    border-radius: 30px;
  }
}

@media (max-width: 992px) {
  .nav-btn.prev { left: -15px; }
  .nav-btn.next { right: -15px; }
  
  .image-wrapper {
    height: 400px;
  }
}

@media (max-width: 768px) {
  .services-content-wrapper {
    padding: 4rem 1.5rem;
    border-radius: 40px;
  }
  
  .services-content-wrapper::after {
    width: 280px;
    top: -50px;
    height: 140px;
  }

  .nav-btn {
    width: 44px;
    height: 44px;
    font-size: 1rem;
  }

  .nav-btn.prev { left: 10px; }
  .nav-btn.next { right: 10px; }

  .image-wrapper {
    height: 300px;
    border-radius: 16px;
  }
  
  .category-selectors {
    gap: 0.5rem;
  }
  
  .filter-btn {
    padding: 0.6rem 1.25rem;
    font-size: 0.85rem;
  }
}
</style>
