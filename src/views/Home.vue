<template>
  <div class="home">
    <div id="hero" class="hero-section">
      <div class="animated-bg" ref="animatedBg"></div>
      <div class="hero-content">
        <h1>Hello, I'm <span class="highlight">Agampreet Singh</span></h1>
        <p class="title">Software Engineer</p>
        <div class="cta-buttons">
          <a href="#projects" class="btn">View My Work</a>
          <a href="#contact" class="btn btn-outline">Contact Me</a>
        </div>
      </div>
    </div>
    
    <AboutSection id="about" />
    <ExperienceSection id="experience" />
    <ProjectsSection id="projects" />
    <SkillsSection id="skills" />
    <ContactSection id="contact" />
  </div>
</template>

<script>
import { onMounted, ref } from 'vue';
import * as THREE from 'three';
import AboutSection from '../components/AboutSection.vue';
import ExperienceSection from '../components/ExperienceSection.vue';
import ProjectsSection from '../components/ProjectsSection.vue';
import SkillsSection from '../components/SkillsSection.vue';
import ContactSection from '../components/ContactSection.vue';

export default {
  name: 'Home',
  components: {
    AboutSection,
    ExperienceSection,
    ProjectsSection,
    SkillsSection,
    ContactSection
  },
  setup() {
    const animatedBg = ref(null);
    
    onMounted(() => {
      initThreeJsBackground();
    });
    
    const initThreeJsBackground = () => {
      const scene = new THREE.Scene();
      const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
      camera.position.z = 30;
      
      const renderer = new THREE.WebGLRenderer({ alpha: true, antialias: true });
      renderer.setSize(window.innerWidth, window.innerHeight);
      animatedBg.value.appendChild(renderer.domElement);
      
      // Particles
      const particlesGeometry = new THREE.BufferGeometry();
      const particlesCount = 1000;
      
      const posArray = new Float32Array(particlesCount * 3);
      for(let i = 0; i < particlesCount * 3; i++) {
        posArray[i] = (Math.random() - 0.5) * 100;
      }
      
      particlesGeometry.setAttribute('position', new THREE.BufferAttribute(posArray, 3));
      
      const particlesMaterial = new THREE.PointsMaterial({
        size: 0.05,
        color: 0x4361ee
      });
      
      const particlesMesh = new THREE.Points(particlesGeometry, particlesMaterial);
      scene.add(particlesMesh);
      
      // Animation
      const animate = () => {
        requestAnimationFrame(animate);
        
        particlesMesh.rotation.x += 0.0005;
        particlesMesh.rotation.y += 0.0005;
        
        renderer.render(scene, camera);
      };
      
      animate();
      
      // Handle resize
      window.addEventListener('resize', () => {
        camera.aspect = window.innerWidth / window.innerHeight;
        camera.updateProjectionMatrix();
        renderer.setSize(window.innerWidth, window.innerHeight);
      });
    };
    
    return {
      animatedBg
    };
  }
}
</script>

<style scoped>
.home {
  width: 100%;
}

.hero-section {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
}

.animated-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
}

.hero-content {
  text-align: center;
  z-index: 1;
  animation: fadeIn 1s ease;
}

.hero-content h1 {
  font-size: 4rem;
  margin-bottom: 20px;
}

.hero-content .title {
  font-size: 1.5rem;
  margin-bottom: 40px;
  color: var(--text-secondary);
}

.highlight {
  background: linear-gradient(to right, var(--primary), var(--accent));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.cta-buttons {
  display: flex;
  gap: 20px;
  justify-content: center;
}

.btn-outline {
  background: transparent;
  border: 2px solid var(--primary);
  box-shadow: none;
}

.btn-outline:hover {
  background: linear-gradient(to right, var(--primary), var(--accent));
}

@media (max-width: 768px) {
  .hero-content h1 {
    font-size: 2.5rem;
  }
  
  .hero-content .title {
    font-size: 1.2rem;
  }
  
  .cta-buttons {
    flex-direction: column;
    align-items: center;
  }
}
</style>