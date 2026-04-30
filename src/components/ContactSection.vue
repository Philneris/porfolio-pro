<template>
  <section id="contact">
    <div class="container">
      <div class="cta-card">
        <div class="cta-content">
          <h2>Contactez-moi</h2>

          <div class="contact-methods">
            <a href="mailto:nerisphil@gmail.com" class="contact-card">
              <div class="contact-icon">
                <i class="fas fa-envelope"></i>
              </div>
              <div>
                <span class="contact-label">Email</span>
                <span class="contact-value">nerisphil@gmail.com</span>
              </div>
            </a>

            <a href="tel:+2290141219117" class="contact-card">
              <div class="contact-icon icon-teal">
                <i class="fas fa-phone-alt"></i>
              </div>
              <div>
                <span class="contact-label">Téléphone</span>
                <span class="contact-value">+229 01 41 21 91 17</span>
              </div>
            </a>

            <a href="https://wa.me/22941219117" target="_blank" class="contact-card">
              <div class="contact-icon icon-whatsapp">
                <i class="fab fa-whatsapp"></i>
              </div>
              <div>
                <span class="contact-label">WhatsApp</span>
                <span class="contact-value">+229 41 21 91 17</span>
              </div>
            </a>

            <a href="https://www.linkedin.com/in/neris-assogbadjo-13270b374/" target="_blank" class="contact-card">
              <div class="contact-icon icon-blue">
                <i class="fab fa-linkedin-in"></i>
              </div>
              <div>
                <span class="contact-label">LinkedIn</span>
                <span class="contact-value">neris-assogbadjo</span>
              </div>
            </a>
          </div>

          <div class="cta-btns">
            <a href="mailto:nerisphil@gmail.com" class="btn btn-primary btn-lg">
              <i class="fas fa-paper-plane"></i> Email
            </a>
            <a href="https://wa.me/22941219117" target="_blank" class="btn btn-whatsapp btn-lg">
              <i class="fab fa-whatsapp"></i> WhatsApp
            </a>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.cta-card {
  background: var(--bg-card);
  border-radius: 24px;
  padding: 50px 30px;
  text-align: center;
  border: 1px solid var(--border-light);
}

.cta-content {
  position: relative;
  z-index: 1;
}

.cta-emoji {
  font-size: 3rem;
  display: block;
  margin-bottom: 1.5rem;
}

.cta-content h2 {
  font-size: 2.5rem;
  margin-bottom: 1rem;
  color: var(--dark);
}

.cta-content > p {
  color: var(--text-muted);
  font-size: 1.1rem;
  margin-bottom: 3rem;
}

.contact-methods {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1.25rem;
  max-width: 1000px;
  margin: 0 auto 3rem;
}

.contact-card {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1.25rem;
  text-align: left;
  background: var(--bg-main);
  border-radius: 20px;
  border: 1px solid var(--border-light);
  transition: var(--ease);
  cursor: pointer;
  text-decoration: none;
}

.contact-card:hover {
  border-color: var(--red);
  transform: translateY(-5px);
  box-shadow: 0 10px 30px rgba(0,0,0,0.05);
}

.contact-icon {
  width: 48px;
  height: 48px;
  border-radius: 14px;
  background: rgba(221, 45, 74, 0.1);
  color: var(--red);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.35rem;
  flex-shrink: 0;
}

.icon-teal {
  background: rgba(154, 213, 202, 0.15);
  color: #3a9b8a;
}

.icon-blue {
  background: rgba(10, 102, 194, 0.1);
  color: #0A66C2;
}

.icon-whatsapp {
  background: rgba(37, 211, 102, 0.1);
  color: #25D366;
}

.contact-label {
  display: block;
  font-size: 0.75rem;
  color: var(--text-muted);
  margin-bottom: 0.15rem;
}

.contact-value {
  font-size: 0.9rem;
  font-weight: 700;
  color: var(--dark);
}

.cta-btns {
  display: flex;
  justify-content: center;
  gap: 1.5rem;
}

.btn-lg {
  padding: 1rem 2.5rem;
  font-size: 1rem;
  display: inline-flex;
  align-items: center;
  gap: 0.75rem;
}

.btn-whatsapp {
  background: #25D366;
  color: white;
  border-radius: 50px;
  font-weight: 700;
  transition: var(--ease);
  box-shadow: 0 10px 30px rgba(37, 211, 102, 0.2);
}

.btn-whatsapp:hover {
  background: #128C7E;
  transform: translateY(-3px);
  box-shadow: 0 15px 40px rgba(37, 211, 102, 0.3);
}

@media (max-width: 1100px) {
  .contact-methods {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .cta-card {
    padding: 3.5rem 1.5rem;
  }

  .cta-content h2 {
    font-size: 1.8rem;
  }

  .contact-methods {
    grid-template-columns: 1fr;
    gap: 1rem;
  }

  .cta-btns {
    flex-direction: column;
    gap: 1rem;
  }

  .btn-lg {
    width: 100%;
    justify-content: center;
  }
}
</style>
