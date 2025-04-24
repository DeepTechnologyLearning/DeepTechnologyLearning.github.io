<template>
    <div class="content">
        <div class="area">
            <div class="left">
                <div 
                    v-for="(domaine) in domainesData" 
                    :key="domaine.id" 
                    class="button-domaines"
                    @click="selectDomaine(domaine.id)"
                    :class="{ active: selectedDomaineId === domaine.id }"
                >
                    {{ String(domaine.id).padStart(2, '0') }}
                </div>
            </div>
            <div class="center">
                <div v-if="selectedDomaine">
                    <div class="card-categorie">
                        <h1 class="card-categorie-number">{{ String(selectedDomaine.id).padStart(2, '0') }}</h1>
                        <h1 class="card-categorie-title">{{ selectedDomaine.domaines }}</h1>
                        <p class="card-categorie-description">{{ selectedDomaine.description }}</p>
                        <p class="card-categorie-description">{{ selectedDomaine.note }}</p>
                        <div class="more">
                            <button class="modern-button" @click="handleButtonClick">
                                <span class="button-text">En savoir +</span>
                            </button>
                        </div>
                    </div>
                </div>
                
            </div>
            <div class="right">
                <div class="right-container" v-if="!isLoading">
                    <div class="carousel-container">
                        <div class="sdomaines-wrapper">
                            <div 
                                class="B" 
                                v-for="(sdomaine, index) in getVisibleItems" 
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
                                v-for="(sdomaine, index) in selectedDomaine?.sdomaines || []" 
                                :key="index"
                                class="pagination-dot"
                                :class="{ active: currentSousDomaineIndex === index }"
                                @click="goToSousDomaine(index)"
                            ></div>
                        </div>
                        <div class="swipe">
                            <button 
                                class="nav-button prev" 
                                @click="previousSousDomaine"
                                :disabled="isTransitioning"
                            >
                                <span class="nav-icon">←</span>
                            </button>
                            <button 
                                class="nav-button next" 
                                @click="nextSousDomaine"
                                :disabled="isTransitioning"
                            >
                                <span class="nav-icon">→</span>
                            </button>
                        </div>
                    </div>
                </div>
                <div class="loader-container" v-if="showLoader">
                    <div class="loader"></div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import domainesData from './Section_3/data/data.json'

export default {
  name: 'Section_3',
  data() {
    return {
            domainesData: domainesData,
            id:null,
            selectedDomaineId: null,
            isLoading: false,
            showLoader: false,
            currentSousDomaineIndex: 0,
            isTransitioning: false
        }
    },
    computed: {
        selectedDomaine() {
            return this.domainesData.find(d => d.id === this.selectedDomaineId)
        },
        getVisibleItems() {
            const items = this.selectedDomaine?.sdomaines || [];
            const currentIndex = this.currentSousDomaineIndex;
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
        }
    },
    methods: {
        selectDomaine(domaineId) {
            this.selectedDomaineId = domaineId;
            this.currentSousDomaineIndex = 0;
        },
        handleButtonClick() {
            this.showLoader = true
            this.isLoading = true
            
            setTimeout(() => {
                this.showLoader = false
                this.isLoading = false
            }, 1500)
        },
        nextSousDomaine() {
            if (this.isTransitioning) return;
            this.isTransitioning = true;
            
            const items = this.selectedDomaine?.sdomaines || [];
            if (!items.length) {
                this.isTransitioning = false;
                return;
            }

            const maxIndex = items.length - 1;
            this.currentSousDomaineIndex = (this.currentSousDomaineIndex + 1) % (maxIndex + 1);
            
            setTimeout(() => {
                this.isTransitioning = false;
            }, 300);
        },
        previousSousDomaine() {
            if (this.isTransitioning) return;
            this.isTransitioning = true;
            
            const items = this.selectedDomaine?.sdomaines || [];
            if (!items.length) {
                this.isTransitioning = false;
                return;
            }

            const maxIndex = items.length - 1;
            this.currentSousDomaineIndex = (this.currentSousDomaineIndex - 1 + maxIndex + 1) % (maxIndex + 1);
            
            setTimeout(() => {
                this.isTransitioning = false;
            }, 300);
        },
        goToSousDomaine(index) {
            if (this.isTransitioning) return;
            this.isTransitioning = true;
            
            const items = this.selectedDomaine?.sdomaines || [];
            if (!items.length) {
                this.isTransitioning = false;
                return;
            }

            this.currentSousDomaineIndex = index;
            
            setTimeout(() => {
                this.isTransitioning = false;
            }, 300);
        }
    }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Lexend+Deca:wght@200;400;500;600;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Mate+SC&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Jones&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Ubuntu:ital,wght@0,300;0,400;0,500;0,700;1,300;1,400;1,500;1,700&family=Work+Sans:ital,wght@0,100..900;1,100..900&display=swap');

.content {
    position: relative;
    display: flex;
    justify-content: space-between;
    align-items: center;
    min-height: 100vh;
    
    background-color: #000;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 20px 0;
}

.area {
    display: flex;
    align-items: center;
    height: 100%;
    width: calc(100% - 180px);
    overflow: hidden;
    background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.98)),url('@/components/home/Section_3/ImgBg/14.jpg');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    background-attachment: fixed; 
    padding: 40px 0;
}

.button-domaines {
    width: 100px;
    height: 100px;
    background-color: transparent;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2rem;
    font-weight: bold;
    cursor: pointer;
    transition: all 0.3s ease;
    margin: 10px 0;
    color:#fff;
    border: 1px solid rgba(255, 255, 255, 0.15);
    
}

.button-domaines:hover {
    transform: scale(1.1);
    border: 1px solid rgba(255, 255, 255, 0.5);
}

.button-domaines.active {
    background-color: rgba(255, 255, 255, 0.1);
    border: 1px solid rgba(255, 255, 255, 0.8);
}

.left{
    padding: 0 20px;
    border-right: 1px solid rgba(255, 255, 255, 0.15);
}

.sous-domaines-container {
    display: flex;

    width: 100%;
}

.sous-domaine-card {
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 255, 255, 0.1);
    padding: 20px;
    border-radius: 10px;
    transition: all 0.3s ease;
}

.sous-domaine-card:hover {
    transform: translateY(-5px);
    background: rgba(255, 255, 255, 0.1);
    border: 1px solid rgba(255, 255, 255, 0.2);
}

.sous-domaine-card h3 {
    color: #fff;
    font-size: 1.5rem;
    margin-bottom: 10px;
}

.sous-domaine-card p {
    color: rgba(255, 255, 255, 0.8);
    font-size: 1rem;
    line-height: 1.5;
}

.sous-domaine-details {
    margin-top: 15px;
    padding-top: 15px;
    border-top: 1px solid rgba(255, 255, 255, 0.1);
}

.center {
    padding: 20px 0;
}

.caroussel-item {
  width: 100%;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    gap: 20px;
    position: relative;
    overflow: hidden;
}


.card-categorie {
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  justify-content: space-between;
  color: #fff;
  padding: 0 2rem;
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

.modern-button {
  background: linear-gradient(45deg, #4d9fff, #0066cc);
  border: none;
  padding: 12px 30px;
  display: flex;
  align-items: center;
  gap: 10px;
  cursor: pointer;
  transition: all 0.3s ease;
  border-radius: 8px;
  position: relative;
  overflow: hidden;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
}

.modern-button::before {
  content: '';
  position: absolute;
  top: 0;
  left: -100%;
  width: 100%;
  height: 100%;
  background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent);
  transition: 0.5s;
}

.modern-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
}

.modern-button:hover::before {
  left: 100%;
}

.modern-button:active {
  transform: translateY(1px);
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
}

.button-text {
    font-family: "Work Sans", sans-serif;
  color: #fff;
  font-size: 1rem;
  font-weight: 500;
  position: relative;
  z-index: 1;
}

.right {
  padding: 0 20px;
  border-left: 1px solid rgba(255, 255, 255, 0.15);
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  width: 100%;
}

.right-container {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.loader-container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 10;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
}

.loader {
  width: 50px;
  height: 50px;
  border: 3px solid rgba(255, 255, 255, 0.1);
  border-radius: 50%;
  border-top-color: #fff;
  animation: spin 1.5s linear infinite;
}

@keyframes spin {
    0% {
        transform: rotate(0deg);
    }
    100% {
        transform: rotate(360deg);
    }
}

.carousel-container {
    position: relative;
    width: 100% ;
    overflow: hidden;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px 0;
    border: 0.1px solid rgba(255, 255, 255, .2);
    margin: 0 auto;
}

.sdomaines-wrapper {
    display: flex;
    gap: 20px;
}

.B {
    flex-shrink: 0;
    width: 150px;
    height: 500px;
    background-image: url('@/components/home/Section_3/ImgBg/15.jpg');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    opacity: .3;
    filter: blur(35px);
    transition: opacity 0.3s ease;
    border-radius: 20px;
}

.B.active {
    opacity: 1;
    filter: blur(0px);
    border-radius: 0px;
    width: 350px;
}

.swipe {
    position: absolute;
    top: 50%;
    left: 0;
    right: 0;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 20px;
    transform: translateY(-50%);
    z-index: 10;
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

</style> 