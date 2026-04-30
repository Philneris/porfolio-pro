<template>
  <section id="competences" class="skills-section">
    <div class="container">
      <div class="section-title">
        <div class="accent-line"></div>
        <h2>Compétences & Outils</h2>
        <p>Les technologies que j'utilise au quotidien</p>
      </div>

      <div class="skills-categories">
        <div
          v-for="(cat, i) in categories"
          :key="cat.title"
          class="skill-category glass-card"
        >
          <div class="cat-header">
            <div class="cat-icon" :style="{ background: cat.iconBg, color: cat.iconColor }">
              <i :class="cat.icon"></i>
            </div>
            <h3>{{ cat.title }}</h3>
          </div>
          <div class="cat-skills">
            <div
              v-for="skill in cat.skills"
              :key="skill.name"
              class="skill-chip"
            >
              <i v-if="skill.icon" :class="skill.icon" :style="{ color: skill.color || 'var(--text-muted)' }"></i>
              <span>{{ skill.name }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
const categories = [
  {
    title: 'Backend',
    icon: 'fas fa-server',
    iconBg: 'rgba(221, 45, 74, 0.1)',
    iconColor: 'var(--red)',
    skills: [
      { name: 'PHP', icon: 'fab fa-php', color: '#8993be' },
      { name: 'Laravel', icon: 'fab fa-laravel', color: '#FF2D20' },
      { name: 'Eloquent ORM' },
      { name: 'Livewire' },
      { name: 'RESTful APIs', icon: 'fas fa-plug', color: 'var(--teal)' },
      { name: 'MVC Architecture' },
    ]
  },
  {
    title: 'Frontend',
    icon: 'fas fa-palette',
    iconBg: 'rgba(154, 213, 202, 0.1)',
    iconColor: 'var(--teal)',
    skills: [
      { name: 'HTML5', icon: 'fab fa-html5', color: '#E34F26' },
      { name: 'CSS3', icon: 'fab fa-css3-alt', color: '#1572B6' },
      { name: 'JavaScript', icon: 'fab fa-js-square', color: '#F7DF1E' },
      { name: 'Vue.js', icon: 'fab fa-vuejs', color: '#4FC08D' },
      { name: 'Tailwind CSS', color: '#06B6D4' },
      { name: 'Bootstrap', icon: 'fab fa-bootstrap', color: '#7952B3' },
      { name: 'Inertia.js' },
    ]
  },
  {
    title: 'Bases de données',
    icon: 'fas fa-database',
    iconBg: 'rgba(255, 229, 0, 0.1)',
    iconColor: 'var(--primary)',
    skills: [
      { name: 'MySQL', icon: 'fas fa-database', color: '#4479A1' },
      { name: 'SQLite', icon: 'fas fa-database', color: 'var(--teal)' },
      { name: 'PostgreSQL', icon: 'fas fa-database', color: '#336791' },
      { name: 'UML / Modélisation' },
    ]
  },
  {
    title: 'Outils & Méthodes',
    icon: 'fas fa-tools',
    iconBg: 'rgba(255, 255, 255, 0.05)',
    iconColor: 'var(--text-white)',
    skills: [
      { name: 'Git', icon: 'fab fa-git-alt', color: '#F05032' },
      { name: 'GitHub', icon: 'fab fa-github' },
      { name: 'JIRA', icon: 'fab fa-jira', color: '#0052CC' },
      { name: 'Responsive Design', icon: 'fas fa-mobile-alt' },
      { name: 'Agile / Scrum' },
      { name: 'Performance', icon: 'fas fa-tachometer-alt', color: 'var(--primary)' },
    ]
  },
]
</script>

<style scoped>
.skills-section {
  background: linear-gradient(180deg, transparent 0%, rgba(48, 50, 61, 0.15) 50%, transparent 100%);
}

.skills-categories {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 2rem;
}

.skill-category {
  padding: 2.5rem;
}

.cat-header {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 1.5rem;
}

.cat-icon {
  width: 50px;
  height: 50px;
  border-radius: 14px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.2rem;
}

.cat-header h3 {
  font-size: 1.2rem;
}

.cat-skills {
  display: flex;
  flex-wrap: wrap;
  gap: 0.6rem;
}

.skill-chip {
  display: inline-flex;
  align-items: center;
  gap: 0.4rem;
  padding: 0.5rem 1rem;
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 10px;
  font-size: 0.85rem;
  font-weight: 500;
  color: var(--text-muted);
  transition: var(--ease);
}

.skill-chip:hover {
  background: rgba(255, 229, 0, 0.08);
  border-color: rgba(255, 229, 0, 0.2);
  color: var(--text-white);
  transform: translateY(-2px);
}

.skill-chip i {
  font-size: 1rem;
}

@media (max-width: 768px) {
  .skills-categories {
    grid-template-columns: 1fr;
  }
}
</style>
