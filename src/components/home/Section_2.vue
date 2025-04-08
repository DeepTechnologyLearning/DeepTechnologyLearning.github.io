<template>
  <section class="section-2">
    <div class="container">
      <h2>Technologies de Pointe</h2>
      <div class="tech-grid">
        <div class="tech-card" v-for="(tech, index) in technologies" :key="index">
          <i :class="tech.icon"></i>
          <h3>{{ tech.title }}</h3>
          <p>{{ tech.description }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Section_2',
  data() {
    return {
      technologies: [
        {
          icon: 'fas fa-brain',
          title: 'Intelligence Artificielle',
          description: 'Découvrez les dernières avancées en IA et machine learning'
        },
        {
          icon: 'fas fa-code',
          title: 'Développement Web',
          description: 'Maîtrisez les frameworks modernes et les bonnes pratiques'
        },
        {
          icon: 'fas fa-shield-alt',
          title: 'Cybersécurité',
          description: 'Protégez vos systèmes contre les menaces modernes'
        }
      ]
    }
  }
}
</script>

<style scoped>
.section-2 {
  padding: 4rem 0;
  background-color: #000;
  color: white;
}

.tech-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  margin-top: 2rem;
}

.tech-card {
  padding: 2rem;
  border-radius: 10px;
  background: #111;
  transition: transform 0.3s ease;
}

.tech-card:hover {
  transform: translateY(-5px);
}

.tech-card i {
  font-size: 2.5rem;
  color: #00ff88;
  margin-bottom: 1rem;
}

.tech-card h3 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: #fff;
}

.tech-card p {
  color: #ccc;
  line-height: 1.6;
}
</style> 