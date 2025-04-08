<template>
  <footer class="section-7">
    <div class="container">
      <div class="footer-content">
        <div class="footer-section">
          <h3>À Propos</h3>
          <p>Deep Technology Learning est une plateforme d'apprentissage en ligne dédiée aux technologies de pointe.</p>
        </div>
        <div class="footer-section">
          <h3>Liens Rapides</h3>
          <ul>
            <li><a href="#">Accueil</a></li>
            <li><a href="#">Cours</a></li>
            <li><a href="#">À propos</a></li>
            <li><a href="#">Contact</a></li>
          </ul>
        </div>
        <div class="footer-section">
          <h3>Contact</h3>
          <ul class="contact-info">
            <li><i class="fas fa-envelope"></i> contact@deeptechlearning.com</li>
            <li><i class="fas fa-phone"></i> +33 1 23 45 67 89</li>
            <li><i class="fas fa-map-marker-alt"></i> Paris, France</li>
          </ul>
        </div>
      </div>
      <div class="footer-bottom">
        <p>&copy; 2024 Deep Technology Learning. Tous droits réservés.</p>
        <div class="social-links">
          <a href="#"><i class="fab fa-facebook"></i></a>
          <a href="#"><i class="fab fa-twitter"></i></a>
          <a href="#"><i class="fab fa-linkedin"></i></a>
          <a href="#"><i class="fab fa-instagram"></i></a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'Section_7'
}
</script>

<style scoped>
.section-7 {
  padding: 4rem 0 2rem 0;
  background-color: #333;
  color: white;
}

.footer-content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
  margin-bottom: 2rem;
}

.footer-section h3 {
  margin-bottom: 1rem;
  color: #fff;
}

.footer-section p {
  color: #ccc;
  line-height: 1.6;
}

.footer-section ul {
  list-style: none;
  padding: 0;
}

.footer-section ul li {
  margin-bottom: 0.5rem;
}

.footer-section a {
  color: #ccc;
  text-decoration: none;
  transition: color 0.3s ease;
}

.footer-section a:hover {
  color: #fff;
}

.contact-info li {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  color: #ccc;
}

.footer-bottom {
  border-top: 1px solid #444;
  padding-top: 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 1rem;
}

.social-links {
  display: flex;
  gap: 1rem;
}

.social-links a {
  color: #ccc;
  font-size: 1.5rem;
  transition: color 0.3s ease;
}

.social-links a:hover {
  color: #fff;
}

@media (max-width: 768px) {
  .footer-bottom {
    flex-direction: column;
    text-align: center;
  }
}
</style> 