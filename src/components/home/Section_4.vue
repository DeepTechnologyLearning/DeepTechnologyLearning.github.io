<template>
  <section class="section-4">
    <div class="container">
      <h2>Témoignages</h2>
      <div class="testimonials">
        <div class="testimonial-card" v-for="(testimonial, index) in testimonials" :key="index">
          <div class="testimonial-content">
            <p class="quote">"{{ testimonial.quote }}"</p>
            <div class="author">
              <img :src="testimonial.avatar" :alt="testimonial.name" class="avatar">
              <div class="author-info">
                <h4>{{ testimonial.name }}</h4>
                <p class="role">{{ testimonial.role }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Section_4',
  data() {
    return {
      testimonials: [
        {
          quote: "Cette plateforme a transformé ma carrière. Les cours sont de qualité exceptionnelle.",
          name: "Marie Dupont",
          role: "Développeuse Full Stack",
          avatar: "https://randomuser.me/api/portraits/women/1.jpg"
        },
        {
          quote: "L'approche pédagogique est innovante et les projets pratiques sont très enrichissants.",
          name: "Jean Martin",
          role: "Data Scientist",
          avatar: "https://randomuser.me/api/portraits/men/1.jpg"
        }
      ]
    }
  }
}
</script>

<style scoped>
.section-4 {
  padding: 4rem 0;
  background-color: #000;
  color: white;
}

.testimonials {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  margin-top: 2rem;
}

.testimonial-card {
  background: #111;
  border-radius: 10px;
  padding: 2rem;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.quote {
  font-style: italic;
  color: #ccc;
  margin-bottom: 1.5rem;
  line-height: 1.6;
}

.author {
  display: flex;
  align-items: center;
}

.avatar {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  margin-right: 1rem;
}

.author-info h4 {
  margin: 0;
  color: #fff;
}

.role {
  color: #ccc;
  margin: 0;
  font-size: 0.9rem;
}
</style>