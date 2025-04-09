<template>
  <section class="hero-section">
    <div class="hero-content">
      <h1 class="hero-title">Deep Technology Learning</h1>
      <p class="hero-subtitle">Explorez les technologies de demain</p>
      <div class="hero-buttons">
        <button class="btn btn-primary">Commencer</button>
        <button class="btn btn-outline">En savoir plus</button>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Section1'
}
</script>

<style scoped>
.hero-section {
  position: relative;
  height: 100vh;
  width: 100%;
  background-image: url('@/assets/HomeImgCpm/18220887_v1016-c-02.png');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  color: #fff;
  padding: 0;
  margin: 0;
  overflow: hidden;
}

.hero-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0);
  z-index: 1;
}

.hero-content {
  position: relative;
  z-index: 2;
  max-width: 800px;
  padding: 0 20px;
}

.hero-title {
  font-size: 4rem;
  font-weight: 700;
  margin-bottom: 1.5rem;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
}

.hero-subtitle {
  font-size: 1.5rem;
  margin-bottom: 2rem;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
}

.hero-buttons {
  display: flex;
  gap: 1rem;
  justify-content: center;
}

.btn {
  padding: 0.75rem 2rem;
  border-radius: 30px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 1px;
  transition: all 0.3s ease;
  cursor: pointer;
}

.btn-primary {
  background: #00ff00;
  border: none;
  color: #000;
}

.btn-primary:hover {
  background: #00cc00;
  transform: translateY(-2px);
}

.btn-outline {
  background: transparent;
  border: 2px solid #00ff00;
  color: #00ff00;
}

.btn-outline:hover {
  background: #00ff00;
  color: #000;
  transform: translateY(-2px);
}

@media (max-width: 768px) {
  .hero-title {
    font-size: 2.5rem;
  }

  .hero-subtitle {
    font-size: 1.2rem;
  }

  .hero-buttons {
    flex-direction: column;
  }

  .btn {
    width: 100%;
    max-width: 300px;
    margin: 0 auto;
  }
}

@media (max-width: 480px) {
  .hero-title {
    font-size: 2rem;
  }

  .hero-subtitle {
    font-size: 1rem;
  }
}
</style> 