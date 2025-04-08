<template>
  <section class="section-5">
    <div class="container">
      <h2>Cours Populaires</h2>
      <div class="courses-grid">
        <div class="course-card" v-for="(course, index) in courses" :key="index">
          <div class="course-image">
            <img :src="course.image" :alt="course.title">
          </div>
          <div class="course-content">
            <h3>{{ course.title }}</h3>
            <p class="description">{{ course.description }}</p>
            <div class="course-meta">
              <span class="duration"><i class="fas fa-clock"></i> {{ course.duration }}</span>
              <span class="level"><i class="fas fa-signal"></i> {{ course.level }}</span>
            </div>
            <button class="enroll-btn">S'inscrire</button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Section_5',
  data() {
    return {
      courses: [
        {
          title: "Introduction à l'IA",
          description: "Découvrez les bases de l'intelligence artificielle et du machine learning",
          duration: "8 semaines",
          level: "Débutant",
          image: "https://images.unsplash.com/photo-1551288049-bebda4e38f71?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
        },
        {
          title: "Développement Web Avancé",
          description: "Maîtrisez les frameworks modernes et les architectures web",
          duration: "12 semaines",
          level: "Intermédiaire",
          image: "https://images.unsplash.com/photo-1498050108023-c5249f4df085?ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60"
        }
      ]
    }
  }
}
</script>

<style scoped>
.section-5 {
  padding: 4rem 0;
  background-color: #ffffff;
}

.courses-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  margin-top: 2rem;
}

.course-card {
  background: white;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.course-card:hover {
  transform: translateY(-5px);
}

.course-image img {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.course-content {
  padding: 1.5rem;
}

.course-content h3 {
  margin: 0 0 1rem 0;
  color: #333;
}

.description {
  color: #666;
  margin-bottom: 1rem;
  line-height: 1.6;
}

.course-meta {
  display: flex;
  justify-content: space-between;
  margin-bottom: 1rem;
  color: #666;
  font-size: 0.9rem;
}

.enroll-btn {
  background: #007bff;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 5px;
  cursor: pointer;
  width: 100%;
  transition: background 0.3s ease;
}

.enroll-btn:hover {
  background: #0056b3;
}
</style> 