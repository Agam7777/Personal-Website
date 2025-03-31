<template>
  <section id="skills" class="section skills-section">
    <div class="container">
      <h2 class="section-title">Skills & Expertise</h2>
      
      <div class="skills-container">
        <div v-for="(category, index) in skillCategories" :key="index" class="skill-category card glow">
          <div class="category-header">
            <div class="category-icon" :style="{ backgroundColor: category.color }">
              <i :class="category.icon"></i>
            </div>
            <h3>{{ category.name }}</h3>
          </div>
          
          <div class="skills-list">
            <div v-for="(skill, skillIndex) in category.skills" :key="skillIndex" class="skill-item">
              <div class="skill-name">{{ skill.name }}</div>
              <div class="skill-bar-container">
                <div class="skill-bar" :style="{ width: `${skill.level}%`, backgroundColor: category.color }"></div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div style="margin-top: 40px;"></div>
      <div class="certifications-section">
        <h3 class="certifications-title">Certifications</h3>
        <div class="certifications-grid">
          <div v-for="(cert, index) in certifications" :key="index" class="certification-card card">
            <div class="certification-icon">
              <i :class="cert.icon"></i>
            </div>
            <div class="certification-details">
              <h4>{{ cert.name }}</h4>
              <p class="certification-issuer">{{ cert.issuer }}</p>
              <p class="certification-year">{{ cert.year }}</p>
            </div>
          </div>
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
  name: 'SkillsSection',
  setup() {
    gsap.registerPlugin(ScrollTrigger);
    
    const skillCategories = ref([
      {
        name: 'Programming Languages',
        icon: 'fas fa-code',
        color: '#4361ee',
        skills: [
          { name: 'Java', level: 95 },
          { name: 'Python', level: 90 },
          { name: 'TypeScript', level: 85 },
          { name: 'JavaScript', level: 85 },
          { name: 'C++', level: 75 },
          { name: 'C#', level: 70 }
        ]
      },
      {
        name: 'Web Development',
        icon: 'fas fa-globe',
        color: '#3a0ca3',
        skills: [
          { name: 'React', level: 85 },
          { name: 'HTML/CSS', level: 90 },
          { name: 'REST APIs', level: 90 },
          { name: 'Spring', level: 85 },
          { name: 'Flask', level: 80 },
          { name: 'Bootstrap', level: 85 }
        ]
      },
      {
        name: 'Database & Query Management',
        icon: 'fas fa-database',
        color: '#7209b7',
        skills: [
          { name: 'MongoDB', level: 90 },
          { name: 'SQL', level: 85 },
          { name: 'GraphQL', level: 80 },
          { name: 'SQLite', level: 85 },
          { name: 'Azure SQL Database', level: 80 },
          { name: 'JDBC', level: 85 }
        ]
      },
      {
        name: 'Data Science & Visualization',
        icon: 'fas fa-chart-line',
        color: '#f72585',
        skills: [
          { name: 'Pandas', level: 85 },
          { name: 'NumPy', level: 80 },
          { name: 'Matplotlib', level: 75 },
          { name: 'Seaborn', level: 75 },
          { name: 'R ShinyApps', level: 70 },
          { name: 'Tableau', level: 85 }
        ]
      },
      {
        name: 'Tools & Deployment',
        icon: 'fas fa-tools',
        color: '#3f8efc',
        skills: [
          { name: 'Docker', level: 80 },
          { name: 'Azure Cloud', level: 75 },
          { name: 'Jira', level: 85 },
          { name: 'Git', level: 90 },
          { name: 'Spinnaker', level: 70 },
          { name: 'Maven', level: 80 }
        ]
      },
      {
        name: 'Testing & QA',
        icon: 'fas fa-vial',
        color: '#fb5607',
        skills: [
          { name: 'JUnit', level: 85 },
          { name: 'Jest', level: 80 },
          { name: 'TDD', level: 75 },
          { name: 'UI Testing', level: 70 },
          { name: 'Integration Testing', level: 75 },
          { name: 'Mock Testing', level: 80 }
        ]
      }
    ]);
    
    const certifications = ref([
      {
        name: 'CCNA Certification',
        issuer: 'Cisco',
        year: '2019',
        icon: 'fas fa-network-wired'
      },
      {
        name: 'Networking Fundamentals',
        issuer: 'Microsoft',
        year: '2019',
        icon: 'fas fa-server'
      },
      {
        name: 'Tableau Data Analytics',
        issuer: 'Duke University',
        year: '2023',
        icon: 'fas fa-chart-pie'
      },
      {
        name: 'Mobility and Device Technology',
        issuer: 'Microsoft',
        year: '2019',
        icon: 'fas fa-mobile-alt'
      }
    ]);
    
    onMounted(() => {
      animateSkills();
    });
    
    const animateSkills = () => {
      // Animate skill categories
      gsap.from('.skill-category', {
        scrollTrigger: {
          trigger: '.skills-section',
          start: 'top 70%',
        },
        y: 50,
        opacity: 0,
        stagger: 0.2,
        duration: 0.5,
        ease: 'power2.out'
      });
      
      // Animate skill bars
      gsap.from('.skill-bar', {
        scrollTrigger: {
          trigger: '.skills-section',
          start: 'top 60%',
        },
        width: 0,
        stagger: 0.05,
        duration: 1,
        ease: 'power2.out',
        delay: 0.5
      });
      
      // Animate certifications
      gsap.from('.certification-card', {
        scrollTrigger: {
          trigger: '.certifications-section',
          start: 'top 90%', // Adjust start position for visibility
          end: 'bottom 10%',
          toggleActions: 'play none none none', // Prevent animations from restarting
        },
      scale: 1,
      opacity: 1,
      stagger: 0.1,
      duration: 0.5,
      ease: 'back.out(1.7)'
      });
    };

    return {
      skillCategories,
      certifications
    };
  }
}
</script>

<style scoped>
.skills-section {
  background-color: var(--background);
  position: relative;
}

.skills-container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(500px, 1fr));
  gap: 30px;
  margin-bottom: 60px;
}

.skill-category {
  padding: 25px;
}

.category-header {
  display: flex;
  align-items: center;
  margin-bottom: 25px;
}

.category-icon {
  width: 50px;
  height: 50px;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-right: 15px;
}

.category-icon i {
  color: white;
  font-size: 1.5rem;
}

.category-header h3 {
  font-size: 1.4rem;
  margin: 0;
}

.skills-list {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.skill-item {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.skill-name {
  font-size: 1rem;
  font-weight: 500;
}

.skill-bar-container {
  width: 100%;
  height: 8px;
  background-color: rgba(255, 255, 255, 0.1);
  border-radius: 4px;
  overflow: hidden;
}

.skill-bar {
  height: 100%;
  border-radius: 4px;
}

.certifications-section {
  margin-top: 100px;
}


.certifications-title {
  text-align: center;
  font-size: 1.8rem;
  margin-bottom: 30px;
  position: relative;
}

.certifications-title::after {
  content: '';
  position: absolute;
  bottom: -10px;
  left: 50%;
  transform: translateX(-50%);
  width: 60px;
  height: 3px;
  background: linear-gradient(to right, var(--primary), var(--accent));
  border-radius: 2px;
}

.certifications-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 25px;
}

.certification-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  padding: 25px 20px;
  transition: all 0.3s ease;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

.certification-card:hover {
  transform: translateY(-10px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
  background-color: rgba(255, 255, 255, 0.1);
}

.certification-icon {
  width: 70px;
  height: 70px;
  background: linear-gradient(45deg, var(--primary), var(--accent));
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 15px;
}

.certification-icon i {
  color: white;
  font-size: 1.8rem;
}

.certification-details h4 {
  font-size: 1.1rem;
  margin-bottom: 8px;
  color: var(--text);
}

.certification-issuer {
  color: var(--text-secondary);
  font-size: 0.9rem;
  margin-bottom: 5px;
}

.certification-year {
  color: var(--primary);
  font-weight: 600;
  font-size: 0.8rem;
}

@media (max-width: 768px) {
  .skills-container {
    grid-template-columns: 1fr;
  }
  
  .certification-card {
    padding: 20px 15px;
  }
  
  .certification-icon {
    width: 60px;
    height: 60px;
  }
}
</style>