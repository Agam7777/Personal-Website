<template>
    <section id="about" class="section about-section">
      <div class="container">
        <h2 class="section-title">About Me</h2>
          
        <div class="about-text" ref="aboutText">
          <p>Hello! I'm Agampreet Singh, a passionate software engineer with a focus on creating innovative solutions. I enjoy tackling complex problems and building applications that make a difference.</p>
          
          <div class="about-details">
            <div class="detail-item">
              <i class="fas fa-envelope"></i>
              <span>agampreet.singh2003@gmail.com</span>
            </div>
            <div class="detail-item">
              <i class="fas fa-phone"></i>
              <span>+1 (425)-598-3133</span>
            </div>
            <div class="detail-item">
              <i class="fas fa-map-marker-alt"></i>
              <span>Seattle, WA</span>
            </div>
            <div class="detail-item">
              <i class="fas fa-id-card"></i>
              <span><b>Interests:</b> Software, AI, Cloud Technologies, and Automation</span>
            </div>
          </div>

            <div class="education-section">
              <h3><i class="fas fa-graduation-cap"></i> Education</h3>
              <div class="education-item card">
                <h4>University of Washington</h4>
                <p class="degree">B.S. in Computer Science and Software Engineering</p>
                <p><span class="highlight">GPA: 3.85</span> (Dean's List x9)</p>
                <p>Expected Graduation: June 2025</p>
                
                <h5>Relevant Coursework:</h5>
                <div class="courses">
                  <span>Data Structures & Algorithms</span>
                  <span>Database Systems</span>
                  <span>Software Engineering Modelling</span>
                  <span>Hardware & Computer Organization</span>
                  <span>Data Science & Analysis</span>
                  <span>Technical Communication</span>
                  <span>Numerical Analysis with Statistics</span>
                  <span>Discrete Mathematics</span>
                </div>
              </div>
            </div>
            
            <div class="social-links">
              <a href="https://www.linkedin.com/in/agampreet-singh1/" target="_blank" class="social-btn">
                <i class="fab fa-linkedin-in"></i> LinkedIn
              </a>
              <a href="https://github.com/Agam7777" target="_blank" class="social-btn">
                <i class="fab fa-github"></i> GitHub
              </a>
            </div>
          </div>
        </div>
    </section>
  </template>
  
  <script>
  import { ref, onMounted } from 'vue';
  import { gsap } from 'gsap';
  import { ScrollTrigger } from 'gsap/ScrollTrigger';
  
  export default {
    name: 'AboutSection',
    setup() {
      gsap.registerPlugin(ScrollTrigger);
      const aboutText = ref(null);
      
      onMounted(() => {
        animateContent();
      });
      
      const animateContent = () => {
        gsap.from('.about-image-container', {
          scrollTrigger: {
            trigger: '.about-section',
            start: 'top 80%',
          },
          x: -100,
          opacity: 0,
          duration: 1,
          ease: 'power3.out'
        });
        
        gsap.from(aboutText.value, {
          scrollTrigger: {
            trigger: '.about-section',
            start: 'top 80%',
          },
          x: 100,
          opacity: 0,
          duration: 1,
          ease: 'power3.out'
        });
      };
      
      return {
        aboutText
      };
    }
  }
  </script>
  
  <style scoped>
  .about-section {
    background-color: var(--surface-light);
    position: relative;
    overflow: hidden;
  }
  
  .about-content {
    display: flex;
    gap: 50px;
    align-items: center;
  }
  
  .about-image-container {
    flex: 1;
    max-width: 400px;
    border-radius: 15px;
    overflow: hidden;
  }
  
  .about-image {
    aspect-ratio: 1 / 1;
    overflow: hidden;
    border-radius: 15px;
    border: 3px solid var(--primary);
  }
  
  .about-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.5s ease;
  }
  
  .about-image:hover img {
    transform: scale(1.05);
  }
  
  .about-text {
    flex: 2;
  }
  
  .about-text p {
    margin-bottom: 20px;
    font-size: 1.1rem;
    line-height: 1.6;
  }
  
  .about-details {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 15px;
    margin-bottom: 30px;
  }
  
  .detail-item {
    display: flex;
    align-items: center;
    gap: 10px;
  }
  
  .detail-item i {
    color: var(--primary);
    font-size: 1.2rem;
  }
  
  .education-section {
    margin-top: 30px;
  }
  
  .education-section h3 {
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    gap: 10px;
  }
  
  .education-section h3 i {
    color: var(--primary);
  }
  
  .education-item {
    margin-bottom: 20px;
  }
  
  .education-item h4 {
    font-size: 1.2rem;
    margin-bottom: 5px;
    color: var(--primary);
  }
  
  .degree {
    font-weight: 500;
    margin-bottom: 5px;
  }
  
  .education-item h5 {
    margin: 15px 0 10px;
  }
  
  .courses {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
  }
  
  .courses span {
    background-color: rgba(67, 97, 238, 0.1);
    padding: 5px 12px;
    border-radius: 20px;
    font-size: 0.9rem;
    border: 1px solid var(--primary);
  }
  
  .social-links {
    display: flex;
    gap: 15px;
    margin-top: 30px;
  }
  
  .social-btn {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 10px 20px;
    background-color: var(--surface);
    color: var(--text);
    text-decoration: none;
    border-radius: 8px;
    transition: all 0.3s ease;
    border: 1px solid var(--primary);
  }
  
  .social-btn:hover {
    background-color: var(--primary);
    transform: translateY(-3px);
  }
  
  @media (max-width: 992px) {
    .about-content {
      flex-direction: column;
      text-align: center;
    }
    
    .about-details {
      grid-template-columns: 1fr;
      justify-items: center;
    }
    
    .courses {
      justify-content: center;
    }
    
    .social-links {
      justify-content: center;
    }
  }
  </style>