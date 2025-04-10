<template>
  <section class="A">
    <div class="video-background">
      <video autoplay muted loop playsinline>
        <source src="@/assets/HomeBgVOC/7020022_Brain_Science_3840x2160.mp4" type="video/mp4">
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

export default {
  name: 'Section1',
  components: {
    VerticalText,
    SocialIcons
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
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.video-background video {
  width: 100%;
  height: 100%;
  object-fit: cover;
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
    position: relative;
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
    margin: 88px 0px 60px 0px;
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
</style> 