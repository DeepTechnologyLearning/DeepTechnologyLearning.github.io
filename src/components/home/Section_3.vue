<template>
  <section class="section-3">
    <div class="content-block">
      <h1>🚀 DÉVELOPPER DES COMPÉTENCES TECHNOLOGIQUES PROFONDES</h1>
      <ul class="features-list">
        <li>🌍 Un savoir-faire avancé pour un avenir prometteur</li>
        <li>🔹 Maîtrisez les bases et les outils avancés</li>
        <li>🔹 Apprenez avec des projets concrets</li>
        <li>🔹 Devenez un expert recherché sur le marché du travail</li>
        <li>🔹 Soyez toujours à la pointe des nouvelles technologies</li>
      </ul>
    </div>
    <div class="content-caroussel">
      <div class="domaine-block" v-for="(domaine, domaineIndex) in domainesData" :key="domaine.id">
        <div class="caroussel-item">
          <div class="A">
            <div class="card-categorie">
              <h1 class="card-categorie-number">{{ String(domaine.id).padStart(2, '0') }}</h1>
              <h1 class="card-categorie-title">{{ domaine.domaines }}</h1>
              <p class="card-categorie-description">{{ domaine.description }}</p>
              <p class="card-categorie-description">{{ domaine.note }}</p>
              <div class="more">
                <button class="modern-button">
                  <span class="button-text">En savoir +</span>
                </button>
                <div class="swipe">
                  <button 
                    class="nav-button prev" 
                    @click="previousSlide(domaineIndex)"
                    :disabled="isTransitioning"
                  >
                    <span class="nav-icon">←</span>
                  </button>
                  <button 
                    class="nav-button next" 
                    @click="nextSlide(domaineIndex)"
                    :disabled="isTransitioning"
                  >
                    <span class="nav-icon">→</span>
                  </button>
                </div>
              </div>
            </div>
          </div>
          <div class="carousel-container">
            <carousel 
              :settings="carouselSettings"
              :breakpoints="{
                768: {
                  itemsToShow: 1.5,
                  paginationEnabled: true
                },
                1024: {
                  itemsToShow: 1.5,
                  paginationEnabled: true
                }
              }"
              :ref="`carousel-${domaineIndex}`"
            >
              <slide v-for="sdomaine in domaine.sdomaines" :key="sdomaine.id">
                <div class="B">
                  <div class="card-scategorie">
                    <div class="top">
                      <div class="left">
                        <h1 class="card-scategorie-number">{{ sdomaine.id }}</h1>
                      </div>
                      <div class="right">
                        <h1 class="card-scategorie-title">{{ sdomaine.nom }}</h1>
                        <p class="card-scategorie-description">{{ sdomaine['des-n'] }}</p>
                      </div>
                    </div>
                    <div class="card-scategorie-description-content">
                      <div class="description-item">{{ sdomaine['des-n-1'] }}</div>
                      <div class="description-item">{{ sdomaine['des-n-2'] }}</div>
                      <div class="description-item">{{ sdomaine['des-n-3'] }}</div>
                      <div class="description-item" v-if="sdomaine['des-n-4']">{{ sdomaine['des-n-4'] }}</div>
                    </div>
                    <span class="card-scategorie-description-content-title">{{ sdomaine.note }}</span>
                  </div>
                </div>
              </slide>
            </carousel>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import domainesData from './Section_3/data/data.json'
import { Carousel, Slide } from 'vue-carousel'

export default {
  name: 'Section_3',
  components: {
    Carousel,
    Slide
  },
  data() {
    return {
      domainesData: domainesData,
      currentSousDomaineIndices: domainesData.map(() => 0),
      isTransitioning: false,
      carouselSettings: {
        itemsToShow: 1.5,
        snapAlign: 'center',
        wrapAround: true,
        transition: 500,
        paginationEnabled: true,
        paginationActiveColor: '#4d9fff',
        paginationColor: 'rgba(255, 255, 255, 0.3)',
        paginationSize: 8,
        paginationPadding: 4
      },
      carouselRefs: {}
    }
  },
  computed: {
    getVisibleItems() {
      return (domaineIndex) => {
        const items = this.domainesData[domaineIndex].sdomaines;
        const currentIndex = this.currentSousDomaineIndices[domaineIndex];
        const length = items.length;

        let visibleItems = [];
        
        // Ajouter l'élément précédent
        visibleItems.push(items[(currentIndex - 1 + length) % length]);
        
        // Ajouter l'élément courant
        visibleItems.push(items[currentIndex]);
        
        // Ajouter l'élément suivant
        visibleItems.push(items[(currentIndex + 1) % length]);

        return visibleItems;
      };
    }
  },
  methods: {
    nextSlide(domaineIndex) {
      const carousel = this.$refs[`carousel-${domaineIndex}`];
      if (carousel) {
        carousel.goToPage(carousel.currentPage + 1);
      }
    },
    previousSlide(domaineIndex) {
      const carousel = this.$refs[`carousel-${domaineIndex}`];
      if (carousel) {
        carousel.goToPage(carousel.currentPage - 1);
      }
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Lexend+Deca:wght@200;400;500;600;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Mate+SC&display=swap');

.swipe{

  display: flex;
  justify-content: space-between;
  align-items: center;
}

.more{
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.modern-button {
  background: transparent;
  border: none;
  padding: 8px 20px;
  display: flex;
  align-items: center;
  gap: 10px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.button-text {
  font-family: 'Mate SC', serif;
  color: #fff;
  font-size: 0.9rem;
}

.button-icon {
  font-family: 'Mate SC', serif;
  color: #4d9fff;
  font-size: 1.2rem;
  transition: transform 0.3s ease;
}

.modern-button:hover .button-icon {
  transform: translateX(5px);
}

.nav-button {
  background: transparent;
  border: none;
  width: 40px;
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
}

.nav-button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.nav-icon {
  font-family: 'Mate SC', serif;
  color: #4d9fff;
  font-size: 1.5rem;
  transition: transform 0.3s ease;
}

.nav-button:hover .nav-icon {
  transform: scale(1.2);
  color: #fff;
}

.content-caroussel {
  margin-top: 50px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  width: calc(100% - 160px);
}

.domaine-block {
  margin-bottom: 4rem;
  width: 100%;
}

.caroussel-item {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
  position: relative;
  overflow: hidden;
}

.carousel-container {
  position: relative;
  width: 720px;

}

.B {
  width: 350px;
  height: 500px;
  background-image: url('@/components/home/Section_3/ImgBg/15.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  margin: 0 auto;
}

.VueCarousel-slide {
  padding: 0 10px;
}

.VueCarousel-pagination {
  position: absolute;
  bottom: -40px;
  left: 50%;
  transform: translateX(-50%);
}

.VueCarousel-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background-color: rgba(255, 255, 255, 0.3);
  margin: 0 4px;
  transition: all 0.3s ease;
}

.VueCarousel-dot--active {
  background-color: #4d9fff;
  transform: scale(1.2);
}

.VueCarousel-navigation-button {
  color: #4d9fff;
  font-size: 2rem;
  transition: all 0.3s ease;
  background: transparent;
  border: none;
  padding: 10px;
  margin: 0;
  cursor: pointer;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  z-index: 10;
}

.VueCarousel-navigation-button:hover {
  color: #fff;
  transform: translateY(-50%) scale(1.2);
}

.VueCarousel-navigation-button:focus {
  outline: none;
}

.VueCarousel-navigation-next {
  right: 20px;
}

.VueCarousel-navigation-prev {
  left: 20px;
}

.VueCarousel {
  position: relative;
  width: 100%;
}

.VueCarousel-wrapper {
  width: 100%;
  position: relative;
  overflow: hidden;
}

.card-categorie {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  justify-content: space-between;
  color: #fff;
  background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),url('@/components/home/Section_3/ImgBg/7.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  padding: 2rem;
  width: 300px;
  height: 390px;
}

.card-categorie * {
  text-align: end;
}

.card-categorie-number{
  font-family: 'Bebas Neue', sans-serif;
  font-size: 3.5rem;
  margin: 0 0 13px 0px;
  color: #fff;
}

.card-categorie-title{
  font-family: 'Bebas Neue', sans-serif;
  font-size: 1.5rem;
  font-weight: 100;
  margin: 0 0 13px 0px;
  color: #fff;
}

.card-categorie-description{
  font-family: 'Lexend Deca', sans-serif;
  font-size: 1rem;
  margin: 0 0 13px 0px;
  color: #fff;
  font-weight: 100;
}

@media (max-width: 1024px) {
  .caroussel-item.A {
    flex-direction: column;
    align-items: center;
  }
}

.section-3 {
  position: relative;
  min-height: 100vh;
  width: 100%;
  overflow: hidden;
  background-image: url('@/components/home/Section_3/ImgBg/1.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  background-attachment: fixed;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 2rem 0;
}

.content-block {
  position: relative;
  z-index: 10;
  width: 100%;
  max-width: 80%;
  padding: 2rem;
  background-image: url('@/components/home/Section_3/ImgBg/2.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.3);
}

h1 {
  text-align:left;
  font-size: 1rem;
  font-weight: 700;
  margin: 0 0 13px 0px;
  color: #fff;
}

.features-list {
  list-style: none;
  padding: 0;
  margin: 0;
}

.features-list li {
  text-align:left;
  font-size: 1rem;
  color: #fff;
  opacity: 0.9;
}

.features-list li:first-child {
  color: #4d9fff;
}

@media (max-width: 768px) {
  .content-block {
    padding: 1.5rem;
  }

  h1 {
    font-size: 1.3rem;
  }

  .features-list li {
    font-size: 0..9rem;
  }
}

.card-scategorie {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 50px 20px;
}

.top {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
}

.left .card-scategorie-number {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 6.5rem;
  font-weight: bold;
  line-height: .5;
  margin: 0;
  color: #000;
}

.right {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.card-scategorie-title {
  font-family: 'Bebas Neue', sans-serif;
  font-size: 1.8rem;
  font-weight: bold;
  margin: 0;
  line-height: 1;
  color: #000;
}

.card-scategorie-description {
  font-family: 'Lexend Deca', sans-serif;
  font-size: 0.8rem;
  margin: 0;
  color: #000;
  text-transform: uppercase;
  line-height: 1.2;
  text-align: left;
}

.card-scategorie-description-content {
    display: flex;
    flex-direction: column;
    margin-bottom: 16px;
    padding: 0;
    text-align: left;
    margin-top: 30px;
}

.description-item {
  font-size: 14px;
  line-height: 1.5;
  color: #666;
  padding-left: 8px;
  position: relative;
}

.description-item::before {
  content: "•";
  position: absolute;
  left: 0;
  color: #4a90e2;
}

.card-scategorie-description-content-title {
  font-family: 'Lexend Deca', sans-serif;
  font-size: 0.8rem;
  color: #000;
  padding-top: 1rem;
}

@media (max-width: 768px) {
  .B {
    padding: 2rem;
  }

  .top {
    gap: 1rem;
  }

  .left .card-scategorie-number {
    font-size: 4rem;
  }

  .card-scategorie-title {
    font-size: 2rem;
  }

  .card-scategorie-description,
  .card-scategorie-description-content {
    font-size: 1rem;
  }
}

@media (max-width: 480px) {
  .B {
    padding: 1.5rem;
  }

  .top {
    flex-direction: column;
    gap: 0.5rem;
  }

  .left .card-scategorie-number {
    font-size: 3rem;
  }

  .card-scategorie-title {
    font-size: 1.75rem;
  }
}
</style> 