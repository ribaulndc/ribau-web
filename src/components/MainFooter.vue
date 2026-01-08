<template>
  <footer class="main-footer">
    <div class="footer-content">
      <!-- Colonna 1: Logo -->
      <div class="footer-col logo-col">
        <div class="logo-lndc">
          <img src="/images/logos/LNDC-Varese_400x128.png" alt="Logo RiBau" style="height: 100px; width: auto;" />
        </div>
      </div>

      <!-- Colonna 2: Dati Associazione -->
      <div class="footer-col association-info">
        <h3>Lega Nazionale Per La Difesa Del Cane</h3>
        <h4>Sezione Di Varese</h4>
        <p>Via Torino, 64, 21013 Gallarate (VA)</p>
        <p>C.F.: 91065410127</p>
        <p>P.IVA: 03569140126</p>
      </div>

      <!-- Colonna 3: Contatti & Link -->
      <div class="footer-col contacts-col">
        <div class="contact-section">
          <h3 class="col-title">Contatti</h3>
          
          <div class="contact-item">
            <img src="/images/icons/email.svg" class="icon" alt="Email" />
            <a href="mailto:caniledivarese@legadelcane-va.com">caniledivarese@legadelcane-va.com</a>
          </div>

          <div class="contact-item">
            <img src="/images/icons/phone.svg" class="icon" alt="Telefono" />
            <a href="tel:+393455787300">+39 3455787300</a>
          </div>

          <div class="contact-item">
            <img src="/images/icons/instagram.svg" class="icon" alt="Instagram" />
            <a href="https://www.instagram.com/caniledivarese_lndcva/" target="_blank">Instagram</a>
          </div>
        </div>
        
        <div class="links-section">
          <h3 class="col-title">Link Utili</h3>
          <p class="privacy-link-container">
            <img src="/images/icons/privacy.svg" class="icon" alt="Privacy" />
            <a href="#/privacy" class="privacy-link">Informativa Privacy</a>
          </p>
          <p class="privacy-link-container">
            <img src="/images/icons/contact-privacy.svg" class="icon" alt="Contact Privacy" />
            <a href="#/contact-privacy" class="privacy-link">Informativa Contatti</a>
          </p>
        </div>
      </div>
    </div>

    <div class="copyright">
      &copy; Copyright 2012 - {{ new Date().getFullYear() }} | Lega Nazionale per la Difesa del Cane - Sezione di Varese
    </div>
  </footer>
</template>

<script>
export default {
  name: 'MainFooter'
}
</script>

<style scoped>
.main-footer {
  background-color: #2c3e50;
  color: white;
  padding: 3rem 1rem 1rem;
  margin-top: auto;
}

.footer-content {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 3rem;
  margin-bottom: 2rem;
}

.footer-col {
  display: flex;
  flex-direction: column;
}

.logo-col {
  align-items: center;
  justify-content: center;
}

.logo-lndc {
  display: flex;
  align-items: center;
  justify-content: center;
}

.association-info {
  align-items: flex-start;
}

h3 {
  color: #42b983;
  font-size: 1.1rem;
  margin: 0 0 0.5rem 0;
  line-height: 1.4;
}

h4 {
  color: #ecf0f1;
  font-size: 1rem;
  margin: 0 0 1rem 0;
  font-weight: normal;
}

.col-title {
  border-bottom: 2px solid #42b983;
  padding-bottom: 0.5rem;
  margin-bottom: 1rem;
  display: inline-block;
  width: fit-content;
}

p {
  margin: 0.25rem 0;
  font-size: 0.9rem;
  color: #bdc3c7;
  line-height: 1.6;
}

.contact-item, .privacy-link-container {
  display: flex;
  align-items: center;
  margin-bottom: 0.8rem;
  color: #bdc3c7;
}

.icon {
  width: 18px;
  height: 18px;
  margin-right: 10px;
  flex-shrink: 0;
  /* Make icons white/grey using filter since they are likely black by default */
  filter: invert(80%) sepia(5%) saturate(0%) hue-rotate(0deg) brightness(90%) contrast(90%);
  transition: filter 0.2s;
}

/* Hover effect for contact items to also color the icon */
.contact-item:hover .icon,
.privacy-link-container:hover .icon {
  /* Greenish filter for #42b983 */
  filter: invert(56%) sepia(38%) saturate(996%) hue-rotate(107deg) brightness(95%) contrast(85%);
}

.links-section {
  margin-top: 2rem;
}

a {
  color: #bdc3c7;
  text-decoration: none;
  transition: color 0.2s;
}

a:hover {
  color: #42b983;
}

.copyright {
  text-align: center;
  margin-top: 2rem;
  padding-top: 1.5rem;
  border-top: 1px solid rgba(255,255,255,0.1);
  font-size: 0.8rem;
  color: #95a5a6;
}

/* Responsive */
@media (max-width: 900px) {
  .footer-content {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 600px) {
  .footer-content {
    grid-template-columns: 1fr;
    text-align: center;
  }
  
  .logo-col {
    order: -1;
    align-items: center;
  }

  .association-info {
    align-items: center;
  }
  
  .col-title {
    margin-left: auto;
    margin-right: auto;
  }

  .contact-item, .privacy-link-container {
    justify-content: center;
  }
}
</style>
