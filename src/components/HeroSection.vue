<template>
  <section id="accueil" class="hero">
    <!-- Decorative colored shapes -->
    <div class="hero-decor">
      <div class="decor-shape shape-rose"></div>
      <div class="decor-shape shape-dark"></div>
    </div>

    <div class="container hero-grid">
      <!-- Left: Text -->
      <div class="hero-text">
        <div class="hero-badge">
          <span class="dot-pulse"></span>
           Développeur web
        </div>
        <h1>
          Je suis <span class="highlight-rose">Néris</span>,<br>
          développeur web<br>
          <span class="typed-text">{{ currentText }}<span class="cursor-blink">|</span></span>
        </h1>
        <p>
          Passionné par l'architecture logicielle et l'optimisation, j'accompagne les entreprises dans la création 
          d'applications robustes, scalables et centrées sur l'expérience utilisateur.
        </p>
        <div class="hero-actions">
          <a href="#projets" class="btn btn-primary">
            <i class="fas fa-briefcase"></i> Voir mes travaux
          </a>
          <a href="#contact" class="btn btn-outline">
            <i class="fas fa-file-alt"></i> Me contacter
          </a>
        </div>
        <div class="hero-stats">
          <div class="stat">
            <span class="stat-number">1+</span>
            <span class="stat-label">Années d'expérience</span>
          </div>
          <div class="stat-divider"></div>
          <div class="stat">
            <span class="stat-number">2</span>
            <span class="stat-label">Projets déployés</span>
          </div>
          <div class="stat-divider"></div>
          <div class="stat">
            <span class="stat-number">100%</span>
            <span class="stat-label">Engagement</span>
          </div>
        </div>
      </div>

      <!-- Right: Photo -->
      <div class="hero-visual">
        <img src="/ma photo.png" alt="Néris - Développeur web" class="hero-photo">
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const words = ['web', 'Full-Stack', 'Laravel', 'Vue.js']
const currentText = ref('')
let wordIndex = 0
let charIndex = 0
let isDeleting = false
let timer = null

const type = () => {
  const currentWord = words[wordIndex]
  if (!isDeleting) {
    currentText.value = currentWord.substring(0, charIndex + 1)
    charIndex++
    if (charIndex === currentWord.length) {
      isDeleting = true
      timer = setTimeout(type, 2000)
      return
    }
  } else {
    currentText.value = currentWord.substring(0, charIndex - 1)
    charIndex--
    if (charIndex === 0) {
      isDeleting = false
      wordIndex = (wordIndex + 1) % words.length
    }
  }
  timer = setTimeout(type, isDeleting ? 50 : 120)
}

onMounted(() => { timer = setTimeout(type, 500) })
onUnmounted(() => { clearTimeout(timer) })
</script>

<style scoped>
.hero {
  min-height: 100vh;
  display: flex;
  align-items: center;
  padding-top: 80px;
  overflow: hidden;
  background: var(--bg-main);
  position: relative;
}

/* -- Decorative BG Shapes -- */
.hero-decor {
  position: absolute;
  inset: 0;
  pointer-events: none;
  z-index: 0;
}

.decor-shape {
  position: absolute;
  border-radius: 50%;
  filter: blur(100px);
}

.shape-rose {
  width: 450px;
  height: 450px;
  background: rgba(221, 45, 74, 0.07);
  top: -10%;
  right: -5%;
}

.shape-dark {
  width: 350px;
  height: 350px;
  background: rgba(48, 50, 61, 0.05);
  bottom: 0;
  left: -5%;
}

/* -- Grid -- */
.hero-grid {
  display: grid;
  grid-template-columns: 1.1fr 0.9fr;
  gap: 4rem;
  align-items: center;
  position: relative;
  z-index: 1;
}

/* -- Badge -- */
.hero-badge {
  display: inline-flex;
  align-items: center;
  gap: 0.6rem;
  background: rgba(221, 45, 74, 0.06);
  border: 1px solid rgba(221, 45, 74, 0.15);
  padding: 0.45rem 1.2rem;
  border-radius: 50px;
  font-size: 0.8rem;
  font-weight: 600;
  color: var(--red);
  margin-bottom: 1.5rem;
  animation: fadeInUp 0.6s ease both;
}

.dot-pulse {
  width: 8px;
  height: 8px;
  background: var(--red);
  border-radius: 50%;
}

/* -- Text -- */
.hero-text h1 {
  font-size: 3.8rem;
  line-height: 1.15;
  margin-bottom: 1.5rem;
  color: var(--dark);
  animation: fadeInUp 0.6s ease 0.2s both;
}

.highlight-rose {
  color: var(--red);
}

.typed-text {
  color: var(--red);
}

.cursor-blink {
  animation: blink 0.8s infinite;
  color: var(--red);
}

@keyframes blink {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}

.hero-text p {
  color: var(--text-muted);
  font-size: 1.1rem;
  max-width: 500px;
  margin-bottom: 2.5rem;
  animation: fadeInUp 0.6s ease 0.4s both;
}

/* -- Actions -- */
.hero-actions {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  margin-bottom: 3rem;
  animation: fadeInUp 0.6s ease 0.6s both;
}

/* -- Stats -- */
.hero-stats {
  display: flex;
  align-items: center;
  gap: 2rem;
  animation: fadeInUp 0.6s ease 0.8s both;
}

.stat-number {
  display: block;
  font-family: 'Space Grotesk', sans-serif;
  font-size: 1.8rem;
  font-weight: 800;
  color: var(--red);
}

.stat-label {
  font-size: 0.8rem;
  color: var(--text-muted);
}

.stat-divider {
  width: 1px;
  height: 40px;
  background: var(--border-light);
}

/* -- Visual / Photo -- */
.hero-visual {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  animation: fadeInUp 0.6s ease 0.3s both;
}

.hero-photo {
  width: 370px;
  height: 370px;
  border-radius: 42% 58% 70% 30% / 45% 45% 55% 55%;
  border: 3px solid rgba(221, 45, 74, 0.2);
  object-fit: cover;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
}

.blob-wrapper {
  position: relative;
}

/* Single deformed ring */
.blob-ring {
  position: absolute;
  inset: -25px;
  border: 2px solid rgba(221, 45, 74, 0.15);
  border-radius: 42% 58% 70% 30% / 45% 45% 55% 55%;
}

.blob {
  width: 370px;
  height: 370px;
  background: rgba(221, 45, 74, 0.03);
  border: 3px solid rgba(221, 45, 74, 0.2);
  border-radius: 42% 58% 70% 30% / 45% 45% 55% 55%;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  position: relative;
}

.abstract-graphic {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  width: 50%;
  position: relative;
}

.bar {
  height: 8px;
  background: var(--red);
  border-radius: 4px;
  opacity: 0.2;
}

.bar-1 { width: 100%; }
.bar-2 { width: 70%; opacity: 0.15; }
.bar-3 { width: 40%; opacity: 0.1; }

.dot {
  position: absolute;
  width: 12px;
  height: 12px;
  background: var(--red);
  border-radius: 50%;
  opacity: 0.4;
}

.dot-1 { top: -20px; right: -10px; }
.dot-2 { bottom: -30px; left: -20px; }

/* -- Responsive -- */
@media (max-width: 992px) {
  .hero-grid {
    grid-template-columns: 1fr;
    text-align: center;
  }

  /* Photo on top on mobile */
  .hero-visual {
    order: -1;
  }

  .hero-text h1 {
    font-size: 2.8rem;
  }

  .hero-text p {
    margin-left: auto;
    margin-right: auto;
  }

  .hero-actions {
    justify-content: center;
  }

  .hero-stats {
    justify-content: center;
  }

  .blob {
    width: 260px;
    height: 260px;
  }

  .blob-ring {
    inset: -18px;
  }

  .hero-badge {
    margin-left: auto;
    margin-right: auto;
  }

  .shape-rose { width: 250px; height: 250px; }
  .shape-dark { width: 200px; height: 200px; }
}

@media (max-width: 480px) {
  .hero-text h1 {
    font-size: 2.2rem;
  }

  .hero-stats {
    gap: 1.5rem;
  }

  .stat-number {
    font-size: 1.5rem;
  }
}
</style>
