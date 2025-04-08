<template>
  <section class="section-3">
    <div class="container">
      <h2>Notre Impact</h2>
      <div class="stats-grid">
        <div class="stat-item" v-for="(stat, index) in stats" :key="index">
          <div class="stat-number">{{ stat.number }}</div>
          <div class="stat-label">{{ stat.label }}</div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Section_3',
  data() {
    return {
      stats: [
        { number: '1000+', label: 'Étudiants Formés' },
        { number: '50+', label: 'Cours Disponibles' },
        { number: '98%', label: 'Taux de Satisfaction' },
        { number: '24/7', label: 'Support Disponible' }
      ]
    }
  }
}
</script>

<style scoped>
.section-3 {
  padding: 4rem 0;
  background-color: #000;
  color: white;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 2rem;
  margin-top: 2rem;
}

.stat-item {
  text-align: center;
}

.stat-number {
  font-size: 3rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
  color: #00ff88;
}

.stat-label {
  font-size: 1.2rem;
  opacity: 0.9;
  color: #ccc;
}
</style> 