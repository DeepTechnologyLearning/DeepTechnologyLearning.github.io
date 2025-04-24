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
            <div class="card-categorie" :style="getDomaineBackground(domaineIndex)">
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
                    @click="previousSousDomaine(domaineIndex)"
                    :disabled="isTransitioning"
                  >
                    <span class="nav-icon">←</span>
                  </button>
                  <button 
                    class="nav-button next" 
                    @click="nextSousDomaine(domaineIndex)"
                    :disabled="isTransitioning"
                  >
                    <span class="nav-icon">→</span>
                  </button>
                </div>
              </div>
            </div>
          </div>
          <div class="carousel-container">
            <div class="sdomaines-wrapper">
              <div 
                class="B" 
                v-for="(sdomaine, index) in getVisibleItems(domaineIndex)" 
                :key="sdomaine.id"
                :class="{ 'active': index === 1 }"
              >
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
            </div>
            <div class="carousel-pagination">
              <div 
                v-for="(sdomaine, index) in domaine.sdomaines" 
                :key="index"
                class="pagination-dot"
                :class="{ active: currentSousDomaineIndices[domaineIndex] === index }"
                @click="goToSousDomaine(domaineIndex, index)"
              ></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import domainesData from '../data/data.json'

export default {
  name: 'Section_3',
  data() {
    return {
      domainesData: domainesData,
      currentSousDomaineIndices: domainesData.map(() => 0),
      isTransitioning: false,
      domaineBackgrounds: [
        "linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),url('@/components/home/Section_3/ImgBg/15.jpg'))",
        "linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),url('@/components/home/Section_3/ImgBg/15.jpg'))",
        "linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),url('@/components/home/Section_3/ImgBg/15.jpg'))",
        "linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)),url('@/components/home/Section_3/ImgBg/15.jpg'))"
      ]
    }
  },
  computed: {
    getVisibleItems() {
      return (domaineIndex) => {
        const items = this.domainesData[domaineIndex]?.sdomaines || [];
        const currentIndex = this.currentSousDomaineIndices[domaineIndex] || 0;
        const length = items.length;

        if (!length) return [];
        if (length === 1) return [items[0], items[0], items[0]];
        if (length === 2) {
          return [
            items[(currentIndex - 1 + 2) % 2],
            items[currentIndex],
            items[(currentIndex + 1) % 2]
          ];
        }

        let visibleItems = [];
        visibleItems.push(items[(currentIndex - 1 + length) % length]);
        visibleItems.push(items[currentIndex]);
        visibleItems.push(items[(currentIndex + 1) % length]);

        return visibleItems;
      };
    }
  },
  methods: {
    nextSousDomaine(domaineIndex) {
      if (this.isTransitioning) return;
      this.isTransitioning = true;
      
      const items = this.domainesData[domaineIndex]?.sdomaines || [];
      if (!items.length) {
        this.isTransitioning = false;
        return;
      }

      const maxIndex = items.length - 1;
      this.currentSousDomaineIndices[domaineIndex] = (this.currentSousDomaineIndices[domaineIndex] + 1) % (maxIndex + 1);
      
      setTimeout(() => {
        this.isTransitioning = false;
      }, 300);
    },
    previousSousDomaine(domaineIndex) {
      if (this.isTransitioning) return;
      this.isTransitioning = true;
      
      const items = this.domainesData[domaineIndex]?.sdomaines || [];
      if (!items.length) {
        this.isTransitioning = false;
        return;
      }

      const maxIndex = items.length - 1;
      this.currentSousDomaineIndices[domaineIndex] = (this.currentSousDomaineIndices[domaineIndex] - 1 + maxIndex + 1) % (maxIndex + 1);
      
      setTimeout(() => {
        this.isTransitioning = false;
      }, 300);
    },
    goToSousDomaine(domaineIndex, index) {
      if (this.isTransitioning) return;
      this.isTransitioning = true;
      
      const items = this.domainesData[domaineIndex]?.sdomaines || [];
      if (!items.length) {
        this.isTransitioning = false;
        return;
      }

      this.currentSousDomaineIndices[domaineIndex] = index;
      
      setTimeout(() => {
        this.isTransitioning = false;
      }, 300);
    },
    getDomaineBackground(domaineIndex) {
      return {
        backgroundImage: this.domaineBackgrounds[domaineIndex % this.domaineBackgrounds.length],
        backgroundSize: 'cover',
        backgroundPosition: 'center',
        backgroundRepeat: 'no-repeat'
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

.nav-button:not(:disabled):hover .nav-icon {
  transform: scale(1.2);
  color: #fff;
}

.content-caroussel {
    margin-top: 50px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: calc(100% - 160px);
}

.domaine-block {
    margin-bottom: 4rem;
    display: flex;
    justify-content: center;
    align-items: center;
}

.caroussel-item {
  width: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 20px;
    position: relative;
    overflow: hidden;
    padding: 0 175px;
}

.carousel-container {
  position: relative;
    width: fit-content;
    overflow: hidden;
    display: flex;
    align-items: center;
    padding: 20px 0;
    border: 0.1px solid rgba(255, 255, 255, .2);
}

.sdomaines-wrapper {
  display: flex;
  gap: 20px;
}

.A{
  border-right: 1px solid rgba(255, 255, 255, .3);
}

.B {
  flex-shrink: 0;
  width: 350px;
  height: 500px;
  background-image: url('@/components/home/Section_3/ImgBg/15.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  opacity: .3;
  filter: blur(35px);
  transition: opacity 0.3s ease;
  border-radius:20px;
}

.B.active {
  opacity: 1;
  filter: blur(0px);
  border-radius:0px;
}

.card-categorie {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  justify-content: space-between;
  color: #fff;
  padding: 2rem;
  width: 300px;
  height: 390px;
  border-radius: 20px;
  transition: all 0.3s ease;
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
  background-image: url('@/components/home/Section_3/ImgBg/14.jpg');
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

.carousel-pagination {
  position: absolute;
  bottom: -40px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  justify-content: center;
  gap: 8px;
  z-index: 10;
  width: 100%;
}

.pagination-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background-color: rgba(255, 255, 255, 0.3);
  cursor: pointer;
  transition: all 0.3s ease;
}

.pagination-dot.active {
  background-color: #4d9fff;
  transform: scale(1.2);
}
</style> 