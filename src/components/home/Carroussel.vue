<!-- components/Carousel.vue -->
<template>
    <div class="carousel-container">
      <div class="carousel">
        <div class="carousel-inner" :style="{ transform: `translateX(-${currentIndex * 100}%)` }">
          <div v-for="(slide, index) in slides" :key="index" class="carousel-slide">
            <div class="card">
              <h3>{{ slide.nom }}</h3>
              <p class="description">{{ slide['des-n'] }}</p>
              <ul class="features">
                <li>{{ slide['des-n-1'] }}</li>
                <li>{{ slide['des-n-2'] }}</li>
                <li>{{ slide['des-n-3'] }}</li>
                <li>{{ slide['des-n-4'] }}</li>
              </ul>
              <p class="note">{{ slide.note }}</p>
            </div>
          </div>
        </div>
      </div>
      
      <div class="carousel-controls">
        <button @click="prev" class="control-btn prev" :disabled="currentIndex === 0">
          &#10094;
        </button>
        <div class="carousel-indicators">
          <span 
            v-for="(_, index) in slides" 
            :key="index"
            :class="['indicator', { active: currentIndex === index }]"
            @click="goToSlide(index)"
          ></span>
        </div>
        <button @click="next" class="control-btn next" :disabled="currentIndex === slides.length - 1">
          &#10095;
        </button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'Carousel',
    props: {
      sdomaines: {
        type: Array,
        required: true
      }
    },
    data() {
      return {
        currentIndex: 0,
        slides: this.sdomaines,
        autoplayInterval: null
      }
    },
    methods: {
      next() {
        if (this.currentIndex < this.slides.length - 1) {
          this.currentIndex++
        }
      },
      prev() {
        if (this.currentIndex > 0) {
          this.currentIndex--
        }
      },
      goToSlide(index) {
        this.currentIndex = index
      },
      startAutoplay() {
        this.autoplayInterval = setInterval(() => {
          if (this.currentIndex === this.slides.length - 1) {
            this.currentIndex = 0
          } else {
            this.next()
          }
        }, 5000)
      },
      stopAutoplay() {
        if (this.autoplayInterval) {
          clearInterval(this.autoplayInterval)
        }
      }
    },
    mounted() {
      this.startAutoplay()
    },
    beforeDestroy() {
      this.stopAutoplay()
    }
  }
  </script>
  
  <style scoped>
  .carousel-container {
    width: 100%;
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
  }
  
  .carousel {
    position: relative;
    overflow: hidden;
    border-radius: 10px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  }
  
  .carousel-inner {
    display: flex;
    transition: transform 0.5s ease;
  }
  
  .carousel-slide {
    min-width: 100%;
    padding: 20px;
  }
  
  .card {
    background: white;
    padding: 2rem;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  }
  
  .card h3 {
    color: #2c3e50;
    margin-bottom: 1rem;
    font-size: 1.5rem;
  }
  
  .description {
    color: #42b983;
    font-size: 1.1rem;
    margin-bottom: 1rem;
  }
  
  .features {
    list-style: none;
    padding: 0;
  }
  
  .features li {
    margin: 0.5rem 0;
    color: #666;
  }
  
  .note {
    margin-top: 1rem;
    color: #e74c3c;
    font-style: italic;
  }
  
  .carousel-controls {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 1rem;
    gap: 1rem;
  }
  
  .control-btn {
    background: #42b983;
    border: none;
    color: white;
    padding: 0.5rem 1rem;
    border-radius: 4px;
    cursor: pointer;
    transition: opacity 0.3s;
  }
  
  .control-btn:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }
  
  .carousel-indicators {
    display: flex;
    gap: 0.5rem;
  }
  
  .indicator {
    width: 10px;
    height: 10px;
    border-radius: 50%;
    background: #ddd;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .indicator.active {
    background: #42b983;
  }
  
  @media (max-width: 768px) {
    .card {
      padding: 1rem;
    }
    
    .card h3 {
      font-size: 1.2rem;
    }
    
    .description {
      font-size: 1rem;
    }
  }
  </style>