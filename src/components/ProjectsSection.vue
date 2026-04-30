<template>
  <section id="projets" class="projects-section">
    <div class="container overflow-visible">
      <div class="projects-content-wrapper">
        <div class="section-container">
          <div class="container title-container">
            <div class="section-title">
              <div class="accent-line"></div>
              <h2>Sélection de Projets</h2>
              <p>Une vitrine de mes travaux techniques récents</p>
            </div>
          </div>

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
              :class="{ active: activeCategory === 'Application Web' }" 
              @click="setCategory('Application Web')">
              App Web
            </button>
            <button 
              class="filter-btn" 
              :class="{ active: activeCategory === 'Outil Web' }" 
              @click="setCategory('Outil Web')">
              Outil Web
            </button>
          </div>

          <!-- Carousel -->
          <div class="carousel-outer">
            <!-- Left arrow -->
            <button class="carousel-btn carousel-btn-left" @click="prevProject" aria-label="Précédent">
              <i class="fas fa-chevron-left"></i>
            </button>

            <div class="carousel-wrapper">
              <transition name="fade" mode="out-in">
                <div
                  v-if="filteredProjects.length > 0"
                  :key="filteredProjects[currentIndex].title"
                  class="carousel-card-single"
                  @click="openLightbox(filteredProjects[currentIndex])"
                >
                  <div class="card-preview">
                    <img :src="filteredProjects[currentIndex].image" :alt="filteredProjects[currentIndex].title" class="project-img" />
                    <div class="click-hint">
                      <i class="fas fa-expand-alt"></i>
                    </div>
                  </div>
                </div>
              </transition>
            </div>

            <!-- Right arrow -->
            <button class="carousel-btn carousel-btn-right" @click="nextProject" aria-label="Suivant">
              <i class="fas fa-chevron-right"></i>
            </button>

            <!-- Indicators -->
            <div class="carousel-indicators" v-if="filteredProjects.length > 1">
              <span 
                v-for="(_, i) in filteredProjects" 
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

    <!-- Lightbox Overlay -->
    <transition name="lightbox-fade">
      <div v-if="isLightboxOpen" class="lightbox-overlay" @click.self="closeLightbox">
        <button class="lightbox-close" @click="closeLightbox" aria-label="Fermer">
          <i class="fas fa-times"></i>
        </button>
        <div class="lightbox-content">
          <img :src="selectedProject?.image" :alt="selectedProject?.title" class="lightbox-img" />
          <div class="lightbox-caption">
            <h3>{{ selectedProject?.title }}</h3>
            <p>{{ selectedProject?.type }}</p>
          </div>
        </div>
      </div>
    </transition>
  </section>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'

const projects = [
  {
    title: 'ATLogistique - Plateforme de suivi de colis en temps réel',
    type: 'Application Web',
    image: '/capture-site-suivi-colis.png',
    gradient: 'linear-gradient(135deg, rgba(221, 45, 74, 0.8) 0%, rgba(48, 50, 61, 0.8) 100%)',
    icon: 'fas fa-shipping-fast',
    badgeClass: 'badge-red',
    url: 'https://atlbenin.com/',
  },
  {
    title: 'New Béthel International School - Site institutionnel scolaire',
    type: 'Site Vitrine',
    image: '/capture-newbethel.png',
    gradient: 'linear-gradient(135deg, rgba(255, 229, 0, 0.8) 0%, rgba(48, 50, 61, 0.8) 100%)',
    icon: 'fas fa-school',
    badgeClass: 'badge-dark',
    url: 'https://newbethelinternationalschool.com/',
  },
  {
    title: 'Simulateur de coût de dédouanement et logistique',
    type: 'Outil Web',
    image: '/capture-simulateur-cout.png',
    gradient: 'linear-gradient(135deg, rgba(48, 50, 61, 0.8) 0%, rgba(26, 26, 46, 0.8) 100%)',
    icon: 'fas fa-calculator',
    badgeClass: 'badge-dark',
  },
  {
    title: 'Luma Botanica - Boutique en ligne de produits naturels',
    type: 'Site Vitrine',
    image: '/site-vitrine-luma_botanica.png',
    gradient: 'linear-gradient(135deg, rgba(121, 85, 72, 0.8) 0%, rgba(48, 50, 61, 0.8) 100%)',
    icon: 'fas fa-leaf',
    badgeClass: 'badge-dark',
  },
  {
    title: 'BeClean - Service professionnel de nettoyage et entretien',
    type: 'Site Vitrine',
    image: '/site-vitrine-beclean.png',
    gradient: 'linear-gradient(135deg, rgba(192, 255, 0, 0.8) 0%, rgba(48, 50, 61, 0.8) 100%)',
    icon: 'fas fa-sparkles',
    badgeClass: 'badge-red',
  },
]

const activeCategory = ref('Tout')
const currentIndex = ref(0)
const isLightboxOpen = ref(false)
const selectedProject = ref(null)
let interval = null

const filteredProjects = computed(() => {
  if (activeCategory.value === 'Tout') return projects
  return projects.filter(project => project.type === activeCategory.value)
})

const nextProject = () => {
  if (filteredProjects.value.length === 0) return
  currentIndex.value = (currentIndex.value + 1) % filteredProjects.value.length
  resetInterval()
}

const prevProject = () => {
  if (filteredProjects.value.length === 0) return
  currentIndex.value = (currentIndex.value - 1 + filteredProjects.value.length) % filteredProjects.value.length
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

const openLightbox = (project) => {
  selectedProject.value = project
  isLightboxOpen.value = true
  document.body.style.overflow = 'hidden' // Stop scrolling
  if (interval) clearInterval(interval)
}

const closeLightbox = () => {
  isLightboxOpen.value = false
  document.body.style.overflow = '' // Resume scrolling
  startInterval()
}

const startInterval = () => {
  if (isLightboxOpen.value) return
  interval = setInterval(() => {
    if (filteredProjects.value.length > 0) {
      currentIndex.value = (currentIndex.value + 1) % filteredProjects.value.length
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
  document.body.style.overflow = ''
})
</script>

<style scoped>
.projects-section {
  padding: 8rem 0;
  overflow: visible;
}

.overflow-visible {
  overflow: visible;
}

.projects-content-wrapper {
  position: relative;
  padding: 6rem 0;
  border-radius: 60% 40% 60% 40% / 65% 65% 35% 35%;
  background: linear-gradient(135deg, rgba(228, 75, 100, 0.05) 0%, rgba(240, 122, 144, 0.1) 100%);
  z-index: 1;
}

.projects-content-wrapper::before {
  content: '';
  position: absolute;
  inset: -15px;
  border: 1.5px solid rgba(228, 75, 100, 0.15);
  border-radius: 45% 55% 35% 65% / 60% 40% 60% 40%;
  z-index: -1;
  pointer-events: none;
  opacity: 0.5;
}

.projects-content-wrapper::after {
  content: '';
  position: absolute;
  top: -50px;
  left: 50%;
  transform: translateX(-50%);
  width: 500px;
  height: 160px;
  background: var(--bg-main);
  border-radius: 50% 50% 0 0;
  z-index: -1;
  border-top: 1.5px solid rgba(228, 75, 100, 0.1);
}

.section-container {
  width: 100%;
}

.title-container {
  max-width: 100%;
  padding: 0 1.5rem;
  position: relative;
  z-index: 2;
  margin-bottom: 2rem;
}

/* Category selectors like ServicesSection */
.category-selectors {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  justify-content: center;
  margin-bottom: 3rem;
  position: relative;
  z-index: 10;
}

.filter-btn {
  padding: 0.75rem 1.5rem;
  border-radius: 50px;
  background: var(--bg-card);
  border: 1px solid var(--border-light);
  color: var(--text-muted);
  font-weight: 700;
  cursor: pointer;
  transition: var(--ease);
  font-size: 0.9rem;
  box-shadow: 0 5px 15px rgba(0,0,0,0.03);
}

.filter-btn:hover {
  border-color: rgba(221, 45, 74, 0.3);
  color: var(--red);
  transform: translateY(-2px);
}

.filter-btn.active {
  background: var(--red);
  color: white;
  border-color: var(--red);
  box-shadow: 0 8px 20px rgba(221, 45, 74, 0.2);
}

.carousel-outer {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 2;
  max-width: 900px;
  margin: 0 auto;
}

.carousel-btn {
  position: absolute;
  z-index: 10;
  width: 48px;
  height: 48px;
  border-radius: 50%;
  background: white;
  border: 1px solid rgba(221, 45, 74, 0.15);
  color: var(--dark);
  font-size: 1rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: var(--ease);
  box-shadow: 0 8px 25px rgba(0,0,0,0.08);
}

.carousel-btn:hover {
  background: var(--red);
  color: white;
  border-color: var(--red);
  transform: scale(1.1);
}

.carousel-btn-left {
  left: -60px;
}

.carousel-btn-right {
  right: -60px;
}

@media (max-width: 1100px) {
  .carousel-btn-left { left: -20px; }
  .carousel-btn-right { right: -20px; }
}

.carousel-wrapper {
  width: 100%;
  min-height: 450px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.carousel-card-single {
  width: 100%;
  max-width: 600px;
  background: var(--bg-card);
  border-radius: 24px;
  overflow: hidden;
  border: 1px solid var(--border-light);
  box-shadow: 0 20px 50px rgba(0, 0, 0, 0.08);
  transition: var(--ease);
  cursor: pointer;
  position: relative;
}

.card-preview {
  height: 350px;
  position: relative;
  overflow: hidden;
}

.project-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.6s ease;
}

.click-hint {
  position: absolute;
  bottom: 1.5rem;
  right: 1.5rem;
  width: 44px;
  height: 44px;
  background: rgba(255, 255, 255, 0.9);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--red);
  font-size: 1.1rem;
  box-shadow: 0 8px 20px rgba(0,0,0,0.1);
  opacity: 0;
  transform: translateY(10px);
  transition: var(--ease);
}

.carousel-card-single:hover .click-hint {
  opacity: 1;
  transform: translateY(0);
}

.carousel-card-single:hover .project-img {
  transform: scale(1.05);
}

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

/* Lightbox Styles */
.lightbox-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.95);
  z-index: 2000;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  cursor: zoom-out;
}

.lightbox-content {
  position: relative;
  max-width: 90vw;
  max-height: 80vh;
  cursor: default;
}

.lightbox-img {
  max-width: 100%;
  max-height: 80vh;
  border-radius: 12px;
  box-shadow: 0 0 50px rgba(0,0,0,0.5);
}

.lightbox-close {
  position: absolute;
  top: 2rem;
  right: 2rem;
  background: white;
  border: none;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  font-size: 1.5rem;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: var(--ease);
  z-index: 2010;
}

.lightbox-close:hover {
  background: var(--red);
  color: white;
  transform: rotate(90deg);
}

.lightbox-caption {
  margin-top: 1.5rem;
  color: white;
  text-align: center;
}

.lightbox-caption h3 {
  font-size: 1.5rem;
  margin-bottom: 0.5rem;
}

.lightbox-caption p {
  color: rgba(255, 255, 255, 0.7);
  font-weight: 600;
}

/* Transitions */
.fade-enter-active, .fade-leave-active { transition: opacity 0.6s ease; }
.fade-enter-from, .fade-leave-to { opacity: 0; }

.lightbox-fade-enter-active, .lightbox-fade-leave-active { transition: opacity 0.4s ease; }
.lightbox-fade-enter-from, .lightbox-fade-leave-to { opacity: 0; }

@media (max-width: 768px) {
  .projects-content-wrapper { padding: 4rem 0.5rem; }
  .carousel-wrapper { min-height: 350px; }
  .carousel-btn-left { left: 0.5rem; }
  .carousel-btn-right { right: 0.5rem; }
  .card-preview { height: 320px; }
  .lightbox-content { max-width: 100%; }
  .lightbox-close { top: 1rem; right: 1rem; width: 40px; height: 40px; font-size: 1.2rem; }
}

@media (max-width: 480px) {
  .card-preview { height: 400px; }
  .carousel-btn-left { left: 1rem; }
  .carousel-btn-right { right: 1rem; }
}
</style>


