<template>
  <section class="section-6">
    <div class="container">
      <div class="newsletter-content">
        <h2>Restez Informé</h2>
        <p>Inscrivez-vous à notre newsletter pour recevoir les dernières actualités et offres spéciales</p>
        <form class="newsletter-form" @submit.prevent="handleSubmit">
          <input 
            type="email" 
            v-model="email" 
            placeholder="Votre adresse email" 
            required
          >
          <button type="submit">S'inscrire</button>
        </form>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Section_6',
  data() {
    return {
      email: ''
    }
  },
  methods: {
    handleSubmit() {
      // Logique d'inscription à la newsletter
      console.log('Email soumis:', this.email);
      this.email = '';
    }
  }
}
</script>

<style scoped>
.section-6 {
  position: relative;
  padding: 4rem 0;
  background-color: #000;
  color: white;
}

.newsletter-content {
  max-width: 600px;
  margin: 0 auto;
  text-align: center;
}

.newsletter-content h2 {
  margin-bottom: 1rem;
  color: #fff;
}

.newsletter-content p {
  margin-bottom: 2rem;
  color: #ccc;
}

.newsletter-form {
  display: flex;
  gap: 1rem;
}

.newsletter-form input {
  flex: 1;
  padding: 0.8rem 1rem;
  border: none;
  border-radius: 5px;
  font-size: 1rem;
  background: #111;
  color: white;
}

.newsletter-form button {
  background: #00ff88;
  color: #000;
  border: none;
  padding: 0.8rem 2rem;
  border-radius: 5px;
  font-weight: bold;
  cursor: pointer;
  transition: background 0.3s ease;
}

.newsletter-form button:hover {
  background: #00cc6a;
}

@media (max-width: 768px) {
  .newsletter-form {
    flex-direction: column;
  }
}
</style> 