<template>
  <section id="about">
    <div class="container about-container">
      <div class="section-title">
        <div class="accent-line"></div>
        <h2>À propos</h2>
      </div>

      <p class="about-text">
        <strong>Ingénieur logiciel</strong> avec une expertise approfondie dans le développement d'écosystèmes web modernes. 
        Je me spécialise dans la conception d'architectures robustes utilisant <strong>Laravel</strong> pour le backend et 
        <strong>Vue.js</strong> pour des interfaces riches et réactives. 
        <br><br>
        Mon approche combine rigueur technique et compréhension des enjeux métier, me permettant de livrer des solutions 
        qui ne se contentent pas de fonctionner, mais qui sont également <strong>performantes, sécurisées et maintenables</strong> sur le long terme.
      </p>
    </div>
  </section>
</template>

<style scoped>
.about-container {
  max-width: 700px;
  text-align: center;
}

.about-text {
  color: var(--text-muted);
  font-size: 1.1rem;
  line-height: 1.9;
}

.about-text strong {
  color: var(--dark);
  font-weight: 600;
}
</style>
