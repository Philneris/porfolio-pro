<template>
  <footer class="footer">
    <div class="container">
      <div class="footer-top">
        <div class="footer-brand">
          <a href="#" class="logo">N<span class="dot">.</span></a>
          <p>Développeur Full-Stack passionné par le code propre et l'innovation.</p>
        </div>
        <div class="footer-nav">
          <a href="#accueil">Accueil</a>
          <a href="#about">À propos</a>
          <a href="#competences">Compétences</a>
          <a href="#experience">Expériences</a>
          <a href="#projets">Projets</a>
          <a href="#contact">Contact</a>
        </div>
      </div>

      <div class="footer-divider"></div>

      <div class="footer-bottom">
        <p>&copy; {{ currentYear }} Néris Assogbadjo — Tous droits réservés.</p>
        <div class="footer-socials">
          <a href="https://www.linkedin.com/in/neris-assogbadjo-13270b374/" target="_blank" aria-label="LinkedIn">
            <i class="fab fa-linkedin-in"></i>
          </a>
          <a href="https://github.com/Philneris" target="_blank" aria-label="GitHub">
            <i class="fab fa-github"></i>
          </a>
          <a href="mailto:nerisphil@gmail.com" aria-label="Email">
            <i class="fas fa-envelope"></i>
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup>
const currentYear = new Date().getFullYear()
</script>

<style scoped>
.footer {
  padding: 3rem 0 2rem;
  border-top: 1px solid var(--border-light);
  background: var(--bg-card);
}

.footer-top {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  flex-wrap: wrap;
  gap: 2rem;
}

.footer-brand .logo {
  font-family: 'Space Grotesk', sans-serif;
  font-size: 1.8rem;
  font-weight: 900;
  display: inline-block;
  margin-bottom: 0.5rem;
  color: var(--dark);
}

.footer-brand .dot {
  color: var(--red);
}

.footer-brand p {
  color: var(--text-muted);
  font-size: 0.9rem;
  max-width: 300px;
}

.footer-nav {
  display: flex;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.footer-nav a {
  color: var(--text-muted);
  font-size: 0.85rem;
  font-weight: 500;
  transition: var(--ease);
}

.footer-nav a:hover {
  color: var(--red);
}

.footer-divider {
  height: 1px;
  background: var(--border-light);
  margin: 2rem 0;
}

.footer-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 1rem;
}

.footer-bottom p {
  color: var(--text-muted);
  font-size: 0.8rem;
}

.footer-socials {
  display: flex;
  gap: 1rem;
}

.footer-socials a {
  width: 40px;
  height: 40px;
  border-radius: 12px;
  background: var(--bg-main);
  border: 1px solid var(--border-light);
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--text-muted);
  transition: var(--ease);
}

.footer-socials a:hover {
  background: var(--red);
  color: var(--white);
  border-color: var(--red);
}

@media (max-width: 768px) {
  .footer-top {
    flex-direction: column;
    align-items: center;
    text-align: center;
  }

  .footer-nav {
    justify-content: center;
  }

  .footer-bottom {
    flex-direction: column;
    text-align: center;
  }
}
</style>
