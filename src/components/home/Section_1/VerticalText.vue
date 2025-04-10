<template>
  <div class="vertical-text-container">
    <div class="vertical-text" v-for="(text, textIndex) in texts" :key="textIndex">
      <span 
        v-for="(letter, index) in text" 
        :key="textIndex + '-' + index" 
        class="digital-text"
        :style="{ animationDelay: index * 0.1 + 's' }"
      >
        {{ randomChar(letter) }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VerticalText',
  data() {
    return {
      texts: ['DEEPTECHNOLOGYLEARNING', 'INTÉLLIGENCE', 'PROFONDE', 'TECHNOLOGIQUE'],
      interval: null
    }
  },
  methods: {
    randomChar(originalChar) {
      const random = Math.random();
      if (random < 0.7) return originalChar;
      return Math.random() < 0.5 ? '0' : '1';
    }
  },
  mounted() {
    this.interval = setInterval(() => {
      this.$forceUpdate();
    }, 100);
  },
  beforeDestroy() {
    if (this.interval) {
      clearInterval(this.interval);
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Share+Tech&display=swap');

.vertical-text-container {
  position: fixed;
  top: 20px;
  left: 13px;
  display: flex;
  z-index: 3;
}

.vertical-text {
  display: flex;
  flex-direction: column;
  gap: 0;
}

span {
  color: #fff;
  font-family: 'Share Tech', sans-serif;
  font-weight: normal;
  font-size: 10px;
  writing-mode: vertical-lr;
  text-orientation: upright;
  text-transform: uppercase;
  height: 11px;
  line-height: 1;
  text-shadow: 0 0 2px rgba(0, 255, 0, 0.5);
  transition: text-shadow 0.3s ease;
}

.vertical-text:hover span {
  text-shadow: 0 0 4px rgba(0, 255, 0, 0.8);
}

@media (max-width: 768px) {
  .vertical-text-container {
    display: none;
  }
}
</style> 