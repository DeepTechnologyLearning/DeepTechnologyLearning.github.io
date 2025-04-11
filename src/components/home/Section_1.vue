<template>
  <section class="A">
    <div class="video-background">
      <!-- Images pour mobile -->
      <div class="mobile-background" v-if="images.length > 0">
        <img 
          v-for="(image, index) in images"
          :key="image"
          :ref="`image${index}`"
          class="background-image"
          :class="{ active: currentImageIndex === index }"
          :src="require(`@/components/home/Section_1/ImgBg/${image}`)"
          alt="Background"
        >
      </div>
      <!-- Vidéos pour desktop -->
      <video 
        v-for="(video, index) in videos"
        :key="video"
        :ref="`video${index}`"
        class="video-player"
        :class="{ active: currentIndex === index }"
        muted 
        playsinline
        loop
      >
        <source :src="require(`@/assets/HomeBgVOC/${video}`)" type="video/mp4">
      </video>
    </div>
    <VerticalText />
    <SocialIcons />
    <div class="AA">
      <h1 class="AAA">APPRENTISSAGE PROFOND TECHNOLOGIQUE</h1>
      <h2 class="AAB">
        FORMEZ-VOUS À L'AVENIR<br>
        MAÎTRISEZ L'IA ET L'INGÉNIERIE LOGICIEL<br>
        AVEC EXPERTISE ET INNOVATION !
      </h2>
      <p class="AAC">
        Embarquez pour une expérience d'apprentissage transformatrice dans la technologie. <br>
        Améliorez votre expertise avec nos cours en ligne compétitifs conçus pour propulser votre carrière vers l'avant
      </p>
      <div class="AAD">
        <div class="AADA">
          <hr/>
          <h3>
            AUTOMATISATION DES COMpétences
          </h3>
          <p>
            Maitrsier les compétences technologique à un prise abordables dès aujourd'hui *
          </p>
        </div>
        <div class="AADB">
          <hr/>
          <h3>
            AUTOMATISATION DES COMpétences
          </h3>
          <p>
            Maitrsier les compétences technologique à un prise abordables dès aujourd'hui *
          </p>
        </div>
        <div class="AADC">
          <hr/>
          <h3>
            AUTOMATISATION DES COMpétences
          </h3>
          <p>
            Maitrsier les compétences technologique à un prise abordables dès aujourd'hui *
          </p>
        </div>
        <div class="AADD">
          <hr/>
          <h3>
            AUTOMATISATION DES COMpétences
          </h3>
          <p>
            Maitrsier les compétences technologique à un prise abordables dès aujourd'hui *
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import VerticalText from './Section_1/VerticalText.vue'
import SocialIcons from './Section_1/SocialIcons.vue'

function importAll(r) {
  return r.keys().map(key => key.slice(2));
}

export default {
  name: 'Section1',
  components: {
    VerticalText,
    SocialIcons
  },
  data() {
    const videoContext = require.context('@/assets/HomeBgVOC', false, /\.(mp4)$/);
    const videos = importAll(videoContext);
    
    let images = [];
    try {
      const imageContext = require.context('@/components/home/Section_1/ImgBg', false, /\.(jpg|jpeg|png|gif)$/);
      images = importAll(imageContext);
    } catch (error) {
      console.warn('Le dossier ImgBg n\'a pas été trouvé ou est vide');
    }
    
    return {
      videos,
      images,
      currentIndex: 0,
      currentImageIndex: 0,
      transitionInterval: null,
      imageInterval: null
    }
  },
  methods: {
    async startVideo(index) {
      try {
        const video = this.$refs[`video${index}`][0];
        if (video) {
          video.currentTime = 0;
          await video.play();
        }
      } catch (error) {
        console.error('Erreur lors de la lecture de la vidéo:', error);
      }
    },
    async switchToNextVideo() {
      const nextIndex = (this.currentIndex + 1) % this.videos.length;
      const nextVideo = this.$refs[`video${nextIndex}`][0];
      
      try {
        await nextVideo.play();
        await new Promise(resolve => setTimeout(resolve, 100));
        this.currentIndex = nextIndex;
      } catch (error) {
        console.error('Erreur lors du changement de vidéo:', error);
      }
    },
    switchToNextImage() {
      if (this.images.length > 0) {
        this.currentImageIndex = (this.currentImageIndex + 1) % this.images.length;
      }
    }
  },
  async mounted() {
    // Démarrer la première vidéo
    await this.startVideo(0);

    // Configurer la transition automatique des vidéos
    this.transitionInterval = setInterval(() => {
      this.switchToNextVideo();
    }, 10000);

    // Configurer la transition automatique des images si elles existent
    if (this.images.length > 0) {
      this.imageInterval = setInterval(() => {
        this.switchToNextImage();
      }, 3500);
    }
  },
  beforeDestroy() {
    if (this.transitionInterval) {
      clearInterval(this.transitionInterval);
    }
    if (this.imageInterval) {
      clearInterval(this.imageInterval);
    }
  }
}
</script>

<style scoped >

.A {
  position: relative;
  height: 100vh;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  text-align: center;
  color: #fff;
  margin: 0;
  overflow: hidden;
}

.video-background {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  z-index: 0;
}

.mobile-background {
  display: none;
}

.background-image {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  opacity: 0;
  transition: opacity 1s ease-in-out;
}

.background-image.active {
  opacity: 1;
}

.video-player {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  opacity: 0;
  transition: opacity 2s ease-in-out;
}

.video-player.active {
  opacity: 1;
}

.A::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.1);
  z-index: 1;
}

.AA {
  position: relative;
  z-index: 2;
  padding: 0 20px;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.AAA {
  font-family: 'Inter', sans-serif;
  font-weight: 700;
  font-size: 20px;
  margin-bottom: 2rem;
  text-transform: uppercase;
  letter-spacing: 2px;
  }

.AAB {
  font-family: 'Inter', sans-serif;
  font-weight: 600;
  font-size: 50px;
  line-height: 1.2;
  margin-bottom: 2rem;
  text-transform: uppercase;
}

.AAC {
  font-family: 'Roboto', sans-serif;
  font-weight: 600;
  font-size: 15px;
  line-height: 1.5;
  margin-bottom: 3rem;
  max-width: 800px;
  margin-left: auto;
  margin-right: auto;
  opacity: 1;
}

.AAD {
    grid-column-gap: 1rem;
    grid-row-gap: 1rem;
    justify-content: flex-start;
    align-self: center;
    align-items: flex-end;
    width: 81vw;
    margin-bottom: 1.6rem;
    display: flex;
    position: absolute;
    bottom: 0;
}

.AADA, .AADB, .AADC, .AADD {
  display: flex;
  flex-direction: column;
  text-align: left;
  opacity: 0.5;
  transition: .7s;
  cursor: pointer;
}


.AADA:hover, .AADB:hover, .AADC:hover, .AADD:hover{
  opacity: 1;
}


.AAD h3, p{
  font-size: 12px;
  text-transform: uppercase;
}

.AAD hr{
  width: 100%;
  margin: 0;
}

@media (max-width: 900px) {
  .AAA {
    font-size: 18px;
  }

  .AAB {
    font-size: 40px;
  }

  .AAC {
    font-size: 14px;
  }

  .AAD {
    position: static;
    align-items: center;
    flex-direction: column;
  }
}

@media (max-width: 480px) {
  .A{
    height: auto;

  }

  .AA{
    position: relative;
    z-index: 2;
    padding: 44px 20px;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background: rgba(0, 0, 0, .3);
    margin: 88px 0px 88px 0px;
  }

  .AAA {
    font-size: 16px;
  }

  .AAB {
    font-size: 30px;
  }

  .AAC {
    font-size: 13px;
  }
}

@media (max-width: 768px) {
  .mobile-background {
    display: block;
  }
  .video-player {
    display: none;
  }
}
</style> 