<template>
  <section id="temoignages" class="testimonials-section">
    <div class="container">
      <div class="testimonials-content-wrapper">
        <div class="section-title">
          <div class="accent-line"></div>
          <h2>Témoignages</h2>
          <p>Ce que mes collaborateurs disent de moi</p>
        </div>

        <div class="carousel-outer">
          <button class="nav-btn prev" @click="prevTestimonial" aria-label="Précédent">
            <i class="fas fa-chevron-left"></i>
          </button>

          <div class="testimonial-wrapper">
            <transition name="fade-slide" mode="out-in">
              <div 
                v-if="testimonials.length > 0"
                :key="currentIndex"
                class="testimonial-card"
              >
                <div class="quote-icon">
                  <i class="fas fa-quote-left"></i>
                </div>
                
                <p class="testimonial-text">
                  {{ testimonials[currentIndex].text }}
                </p>

                <div class="author-info">
                  <div class="author-avatar" :style="{ background: testimonials[currentIndex].gradient }">
                    <i :class="testimonials[currentIndex].icon"></i>
                  </div>
                  <div class="author-details">
                    <h4 class="author-name">{{ testimonials[currentIndex].name }}</h4>
                    <span class="author-role">{{ testimonials[currentIndex].role }}</span>
                  </div>
                </div>
              </div>
            </transition>
          </div>

          <button class="nav-btn next" @click="nextTestimonial" aria-label="Suivant">
            <i class="fas fa-chevron-right"></i>
          </button>

          <!-- Indicators -->
          <div class="carousel-indicators" v-if="testimonials.length > 1">
            <span 
              v-for="(_, i) in testimonials" 
              :key="i" 
              class="dot"
              :class="{ active: currentIndex === i }"
              @click="setCurrentIndex(i)"
            ></span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const testimonials = [
  {
    name: "Alexandre Dupont",
    role: "Propriétaire — ATLogistique",
    text: "Le développement de notre site de suivi de colis a été une expérience exceptionnelle. La réactivité et la qualité technique apportées au projet ont permis de fluidifier nos opérations quotidiennes.",
    icon: "fas fa-user",
    gradient: "linear-gradient(135deg, #FF7A90 0%, #E44B64 100%)"
  },
  {
    name: "Marie-Louise K.",
    role: "Directrice — New Béthel",
    text: "Une collaboration fructueuse pour la refonte de notre plateforme scolaire. Le résultat est moderne, rapide et très facile à utiliser pour les parents comme pour l'administration.",
    icon: "fas fa-user-tie",
    gradient: "linear-gradient(135deg, #FFD000 0%, #FF9500 100%)"
  },
  {
    name: "Jean-Marc S.",
    role: "CEO — Luma Botanica",
    text: "Le site vitrine réalisé capture parfaitement l'essence de notre marque. Le design est épuré et les performances sont au rendez-vous. Je recommande vivement !",
    icon: "fas fa-user-circle",
    gradient: "linear-gradient(135deg, #795548 0%, #30323D 100%)"
  }
]

const currentIndex = ref(0)
let interval = null

const nextTestimonial = () => {
  currentIndex.value = (currentIndex.value + 1) % testimonials.length
  resetInterval()
}

const prevTestimonial = () => {
  currentIndex.value = (currentIndex.value - 1 + testimonials.length) % testimonials.length
  resetInterval()
}

const setCurrentIndex = (i) => {
  currentIndex.value = i
  resetInterval()
}

const startInterval = () => {
  interval = setInterval(() => {
    currentIndex.value = (currentIndex.value + 1) % testimonials.length
  }, 6000)
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
.testimonials-section {
  padding: 8rem 0;
  position: relative;
  overflow: hidden;
}

.testimonials-content-wrapper {
  position: relative;
  max-width: 1000px;
  margin: 0 auto;
}

.section-title {
  margin-bottom: 4rem;
  text-align: center;
}

.carousel-outer {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
}

.nav-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 10;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  border: 1px solid rgba(221, 45, 74, 0.15);
  background: white;
  color: var(--dark);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: var(--ease);
  box-shadow: 0 8px 25px rgba(0,0,0,0.06);
}

.nav-btn:hover {
  background: var(--red);
  color: white;
  border-color: var(--red);
  transform: translateY(-50%) scale(1.1);
  box-shadow: 0 10px 30px rgba(221, 45, 74, 0.2);
}

.nav-btn.prev { left: -70px; }
.nav-btn.next { right: -70px; }

.testimonial-wrapper {
  width: 100%;
  min-height: 380px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.testimonial-card {
  background: var(--bg-card);
  padding: 4rem;
  border-radius: 40px;
  border: 1px solid var(--border-light);
  box-shadow: 0 25px 60px rgba(0, 0, 0, 0.05);
  text-align: center;
  position: relative;
  max-width: 800px;
  transition: var(--ease);
}

.testimonial-card:hover {
  transform: translateY(-5px);
  border-color: rgba(221, 45, 74, 0.2);
}

.quote-icon {
  font-size: 3rem;
  color: var(--red);
  opacity: 0.15;
  margin-bottom: 2rem;
}

.testimonial-text {
  font-size: 1.35rem;
  line-height: 1.8;
  color: var(--dark);
  font-style: italic;
  margin-bottom: 3rem;
  font-weight: 500;
  position: relative;
}

.author-info {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1.25rem;
}

.author-avatar {
  width: 60px;
  height: 60px;
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-size: 1.5rem;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
}

.author-details {
  text-align: left;
}

.author-name {
  font-size: 1.1rem;
  font-weight: 800;
  color: var(--dark);
  margin-bottom: 0.2rem;
}

.author-role {
  font-size: 0.9rem;
  color: var(--text-muted);
  font-weight: 600;
}

/* Indicators */
.carousel-indicators {
  position: absolute;
  bottom: -40px;
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

/* Transitions */
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all 0.6s ease;
}

.fade-slide-enter-from {
  opacity: 0;
  transform: translateX(30px);
}

.fade-slide-leave-to {
  opacity: 0;
  transform: translateX(-30px);
}

@media (max-width: 1100px) {
  .nav-btn.prev { left: -20px; }
  .nav-btn.next { right: -20px; }
  
  .testimonial-card {
    padding: 3rem 2rem;
  }
}

@media (max-width: 768px) {
  .testimonial-text {
    font-size: 1.1rem;
  }
  
  .nav-btn {
    width: 44px;
    height: 44px;
  }

  .nav-btn.prev { left: 0; }
  .nav-btn.next { right: 0; }

  .testimonial-wrapper {
    padding: 0 1rem;
  }
}
</style>
