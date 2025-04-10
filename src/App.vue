<template>
  <div id="app">
    <nav class="main-nav">
      <div class="nav-content">
        <div class="nav-links">
          <img src="@/assets/LogoApp/LogoAppW2.png" width="30" height="30">
        </div>
        <button class="menu-toggle" @click="toggleMenu">
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <line x1="3" y1="12" x2="21" y2="12"></line>
            <line x1="3" y1="6" x2="21" y2="6"></line>
            <line x1="3" y1="18" x2="21" y2="18"></line>
          </svg>
        </button>
      </div>
      <div class="mobile-menu" :class="{ 'active': isMenuOpen }">
        <router-link to="/" @click="closeMenu">Home</router-link>
        <router-link to="/about" @click="closeMenu">About</router-link>
      </div>
    </nav>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      isMenuOpen: false
    }
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    },
    closeMenu() {
      this.isMenuOpen = false;
    }
  }
}
</script>

<style lang="less">
html {
  scrollbar-width: none;
  -ms-overflow-style: none;
}

html::-webkit-scrollbar {
  width: 0;
  opacity: 0;
}

html::-webkit-scrollbar-track {
  background: transparent;
  opacity: 0;
}

html::-webkit-scrollbar-thumb {
  background-color: transparent;
  opacity: 0;
}

body{
  margin: 0;
  overflow-y: auto;
  scrollbar-width: none;
  -ms-overflow-style: none;
}

body::-webkit-scrollbar {
  width: 0;
  opacity: 0;
}

body::-webkit-scrollbar-track {
  background: transparent;
  opacity: 0;
}

body::-webkit-scrollbar-thumb {
  background-color: transparent;
  opacity: 0;
}

#app {
  background-color: #000;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  &::before{
    content: '';
    content: '';
    position: fixed;
    top: 0;
    left: 70px;
    right: 0;
    width: 0.5px;
    opacity: .2;
    height: 100%;
    background: #fff;
    z-index: 1;
  }

  &::after{
    content: '';
    position: fixed;
    top: 0;
    right: 70px;
    width: .5px;
    opacity: .2;
    height: 100%;
    background: #fff;
  }
}

.main-nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  background: transparent;
  padding: 20px 16px 0 106px;
  z-index: 1000;
}

.nav-content {
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.nav-links {
  display: flex;
  gap: 20px;
}

.menu-toggle {
  background: none;
  border: none;
  color: #fff;
  cursor: pointer;
  padding: 0;
  
}

.menu-toggle svg {
  width: 35px;
  height: 35px;
  stroke: #fff;
}

.main-nav a {
  color: #fff;
  text-decoration: none;
  font-weight: 500;
  padding: 8px 16px;
  border-radius: 8px;
  transition: all 0.3s ease;
  
}

.main-nav a:hover {
  background: rgba(255, 255, 255, 0.1);
}

.main-nav a.router-link-exact-active {
  background: rgba(0, 255, 0, 0.2);
  color: #00ff00;
}

.mobile-menu {
  display: none;
  flex-direction: column;
  gap: 10px;
  padding: 20px;
  background: rgba(0, 0, 0, 0.8);
  position: fixed;
  top: 80px;
  right: 0;
  width: 100%;
  transform: translateX(100%);
  transition: transform 0.3s ease;
}

.mobile-menu.active {
  transform: translateX(0);
}

@media (max-width: 768px) {

  .main-nav {
    padding: 20px;
  }

  #app{
    &::before, &::after{
      display: none;
    }
  }


}
</style>
