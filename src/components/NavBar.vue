<template>
  <nav :class="['navbar', { 'navbar-scrolled': scrolled }]">
    <div class="navbar-container">
      <div class="navbar-logo" @click="scrollToTop">
        <span class="logo-text">A<span class="highlight">S</span></span>
      </div>
      
      <div class="menu-toggle" @click="toggleMenu">
        <div :class="['bar', { 'animate': menuOpen }]"></div>
        <div :class="['bar', { 'animate': menuOpen }]"></div>
        <div :class="['bar', { 'animate': menuOpen }]"></div>
      </div>
      
      <div :class="['navbar-links', { 'active': menuOpen }]">
        <a href="#about" @click="closeMenu">About</a>
        <a href="#experience" @click="closeMenu">Experience</a>
        <a href="#projects" @click="closeMenu">Projects</a>
        <a href="#skills" @click="closeMenu">Skills</a>
        <a href="#contact" @click="closeMenu">Contact</a>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'NavBar',
  data() {
    return {
      menuOpen: false,
      scrolled: false
    }
  },
  mounted() {
    window.addEventListener('scroll', this.handleScroll);
  },
  beforeUnmount() {
    window.removeEventListener('scroll', this.handleScroll);
  },
  methods: {
    toggleMenu() {
      this.menuOpen = !this.menuOpen;
      
      // Prevent scrolling when menu is open
      document.body.style.overflow = this.menuOpen ? 'hidden' : '';
    },
    closeMenu() {
      this.menuOpen = false;
      document.body.style.overflow = '';
    },
    handleScroll() {
      this.scrolled = window.scrollY > 50;
    },
    scrollToTop() {
      window.scrollTo({
        top: 0,
        behavior: 'smooth'
      });
    }
  }
}
</script>

<style scoped>
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  padding: 20px 0;
  transition: all 0.3s ease;
  z-index: 1000;
}

.navbar-scrolled {
  background-color: rgba(10, 10, 10, 0.9);
  backdrop-filter: blur(10px);
  padding: 15px 0;
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.1);
}

.navbar-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.navbar-logo {
  cursor: pointer;
}

.logo-text {
  font-size: 2rem;
  font-weight: 700;
  color: var(--text);
}

.highlight {
  color: var(--primary);
}

.navbar-links {
  display: flex;
  gap: 30px;
}

.navbar-links a {
  color: var(--text);
  text-decoration: none;
  font-weight: 500;
  font-size: 1rem;
  position: relative;
  transition: all 0.3s ease;
}

.navbar-links a::after {
  content: '';
  position: absolute;
  width: 0;
  height: 2px;
  bottom: -5px;
  left: 0;
  background: linear-gradient(to right, var(--primary), var(--accent));
  transition: width 0.3s ease;
}

.navbar-links a:hover {
  color: var(--primary);
}

.navbar-links a:hover::after {
  width: 100%;
}

.menu-toggle {
  display: none;
  flex-direction: column;
  justify-content: space-between;
  width: 30px;
  height: 21px;
  cursor: pointer;
}

.bar {
  height: 3px;
  width: 100%;
  background-color: var(--text);
  border-radius: 10px;
  transition: all 0.3s ease;
}

@media (max-width: 768px) {
  .menu-toggle {
    display: flex;
  }
  
  .navbar-links {
    position: fixed;
    top: 0;
    right: -100%;
    width: 70%;
    height: 100vh;
    background-color: var(--surface);
    flex-direction: column;
    justify-content: center;
    align-items: center;
    transition: right 0.3s ease;
    gap: 40px;
  }
  
  .navbar-links.active {
    right: 0;
  }
  
  .bar.animate:nth-child(1) {
    transform: translateY(9px) rotate(45deg);
  }
  
  .bar.animate:nth-child(2) {
    opacity: 0;
  }
  
  .bar.animate:nth-child(3) {
    transform: translateY(-9px) rotate(-45deg);
  }
}
</style>