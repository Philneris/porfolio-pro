<template>
  <header :class="{ scrolled: isScrolled }">
    <nav class="container">
      <a href="#" class="logo">N<span class="logo-dot">.</span></a>

      <ul class="nav-links" :class="{ active: menuOpen }">
        <li v-for="link in links" :key="link.href">
          <a :href="link.href" @click="menuOpen = false">{{ link.label }}</a>
        </li>
      </ul>

      <a href="#contact" class="btn btn-primary nav-cta">
        <i class="fas fa-paper-plane"></i> Contact
      </a>

      <button class="burger" :class="{ open: menuOpen }" @click="menuOpen = !menuOpen" aria-label="Menu">
        <span></span>
        <span></span>
        <span></span>
      </button>
    </nav>
  </header>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const menuOpen = ref(false)

const links = [
  { href: '#accueil', label: 'Accueil' },
  { href: '#about', label: 'À propos' },
  { href: '#competences', label: 'Compétences' },
  { href: '#experience', label: 'Expériences' },
  { href: '#projets', label: 'Projets' },
]

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
}

onMounted(() => window.addEventListener('scroll', handleScroll))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))
</script>

<style scoped>
header {
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 1000;
  transition: var(--ease);
  padding: 0.5rem 0;
}

header.scrolled {
  background: rgba(255, 255, 255, 0.92);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--border-light);
  padding: 0;
  box-shadow: 0 2px 20px rgba(0,0,0,0.04);
}

nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 72px;
}

.logo {
  font-family: 'Space Grotesk', sans-serif;
  font-size: 2rem;
  font-weight: 900;
  color: var(--dark);
  z-index: 1001;
}

.logo-dot {
  color: var(--red);
}

.nav-links {
  display: flex;
  gap: 2.5rem;
}

.nav-links a {
  color: var(--text-muted);
  font-weight: 500;
  font-size: 0.9rem;
  transition: var(--ease);
  position: relative;
}

.nav-links a::after {
  content: '';
  position: absolute;
  bottom: -4px;
  left: 0;
  width: 0;
  height: 2px;
  background: var(--red);
  transition: width 0.3s ease;
}

.nav-links a:hover {
  color: var(--dark);
}

.nav-links a:hover::after {
  width: 100%;
}

.nav-cta {
  padding: 0.6rem 1.5rem;
  font-size: 0.85rem;
}

.burger {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
  z-index: 1001;
  width: 30px;
  height: 24px;
  position: relative;
}

.burger span {
  display: block;
  width: 100%;
  height: 2px;
  background: var(--dark);
  position: absolute;
  left: 0;
  transition: var(--ease);
}

.burger span:nth-child(1) { top: 0; }
.burger span:nth-child(2) { top: 50%; transform: translateY(-50%); }
.burger span:nth-child(3) { bottom: 0; }

.burger.open span:nth-child(1) { top: 50%; transform: translateY(-50%) rotate(45deg); }
.burger.open span:nth-child(2) { opacity: 0; }
.burger.open span:nth-child(3) { bottom: 50%; transform: translateY(50%) rotate(-45deg); }

@media (max-width: 768px) {
  .nav-links {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    background: rgba(255, 255, 255, 0.98);
    backdrop-filter: blur(20px);
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 2rem;
    transform: translateX(100%);
    transition: transform 0.4s ease;
  }

  .nav-links.active {
    transform: translateX(0);
  }

  .nav-links a {
    font-size: 1.5rem;
    color: var(--dark);
  }

  .nav-cta {
    display: none;
  }

  .burger {
    display: block;
  }
}
</style>
