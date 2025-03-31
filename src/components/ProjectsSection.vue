<template>
  <section id="projects" class="section projects-section">
    <div class="container">
      <h2 class="section-title">Personal Projects</h2>
      
      <div class="projects-container">
        <div v-for="(project, index) in projects" :key="index" class="project-card card glow">
          <div class="project-content">
            <h3 class="project-title">{{ project.title }}</h3>
            <div class="project-tech">
              <span v-for="(tech, techIndex) in project.technologies" :key="techIndex" class="tech-tag">
                {{ tech }}
              </span>
            </div>
            <p class="project-description">{{ project.description }}</p>
            <ul class="project-features">
              <li v-for="(feature, featureIndex) in project.features" :key="featureIndex">
                {{ feature }}
              </li>
            </ul>
            <div class="project-links">
              <a :href="project.githubLink" class="project-link" target="_blank" rel="noopener noreferrer">
                <i class="fab fa-github"></i> View Code
              </a>
              <a v-if="project.demoLink" :href="project.demoLink" class="project-link" target="_blank" rel="noopener noreferrer">
                <i class="fas fa-external-link-alt"></i> Live Demo
              </a>
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
  name: 'ProjectsSection',
  setup() {
    gsap.registerPlugin(ScrollTrigger);
    
    const projects = ref([
      {
        title: 'Resume Analyzer',
        technologies: ['Python', 'Flask', 'Bootstrap', 'JavaScript', 'NLP'],
        description: 'An AI-driven NLP system for resume-job description matching that quantifies relevance.',
        features: [
          'Engineered NLP system using SpaCy, NLTK, TF-IDF vectorization, and cosine similarity.',
          'Implemented text analysis for keyword extraction, skill matching, and semantic understanding.',
          'Developed UI with Bootstrap/JavaScript for real-time results visualization and dynamic suggestion rendering.'
        ],
        githubLink: 'https://github.com/Agam7777/resume-analyzer',
        demoLink: ''
      },
      {
        title: 'Task Manager',
        technologies: ['Java', 'TypeScript', 'MongoDB', 'Spring Boot', 'React'],
        description: 'A full-stack Task Manager application with a Java backend and React frontend.',
        features: [
          'Developed a backend using Spring Boot for efficient application configuration and deployment.',
          'Implemented RESTful APIs for robust data handling between the backend and frontend.',
          'Integrated MongoDB Compass for scalable data storage and management.',
          'Built a dynamic and responsive user interface using React.'
        ],
        githubLink: 'https://github.com/Agam7777/task-manager',
        demoLink: ''
      },
      {
        title: 'Patient-Caregiver Reservation Application',
        technologies: ['Java', 'SQL', 'JDBC', 'Azure'],
        description: 'A reservation system connecting patients with caregivers and managing appointments.',
        features: [
          'Designed and managed complex schemas on Microsoft Azure SQL Database for patient records, caregiver details, appointments, and vaccines.',
          'Implemented intricate Java classes on the backend to ensure robust functionality.',
          'Leveraged JDBC for efficient integration with cloud infrastructure, enabling real-time updates.',
          'Created a comprehensive system for managing appointments and vaccine information.'
        ],
        githubLink: 'https://github.com/Agam7777/Vaccine-Scheduler',
        demoLink: ''
      }
    ]);
    
    onMounted(() => {
      animateProjects();
    });
    
    const animateProjects = () => {
      gsap.from('.project-card', {
        scrollTrigger: {
          trigger: '.projects-section',
          start: 'top 70%',
        },
        opacity: 0,
        y: 50,
        stagger: 0.3,
        duration: 0.8,
        ease: 'power2.out'
      });
    };
    
    return {
      projects
    };
  }
}
</script>

<style scoped>
.projects-section {
  background-color: var(--background);
  position: relative;
}

.projects-container {
  display: flex;
  flex-direction: column;
  gap: 40px;
}

.project-card {
  padding: 30px;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  border-left: 4px solid var(--primary);
}

.project-card:nth-child(2) {
  border-left-color: var(--secondary);
}

.project-card:nth-child(3) {
  border-left-color: var(--accent);
}

.project-title {
  font-size: 1.6rem;
  margin-bottom: 15px;
  color: var(--primary);
  position: relative;
  display: inline-block;
}

.project-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 15px;
}

.tech-tag {
  padding: 5px 10px;
  background-color: rgba(67, 97, 238, 0.1);
  border-radius: 20px;
  font-size: 0.8rem;
  border: 1px solid var(--primary);
  white-space: nowrap;
}

.project-description {
  margin-bottom: 15px;
  line-height: 1.6;
  color: var(--text);
}

.project-features {
  list-style-type: none;
  padding: 0;
  margin-bottom: 20px;
}

.project-features li {
  position: relative;
  padding-left: 20px;
  margin-bottom: 10px;
  line-height: 1.5;
  color: var(--text-secondary);
}

.project-features li::before {
  content: '→';
  position: absolute;
  left: 0;
  color: var(--primary);
  font-weight: bold;
}

.project-links {
  display: flex;
  gap: 15px;
  margin-top: 20px;
}

.project-link {
  display: inline-flex;
  align-items: center;
  padding: 8px 15px;
  background-color: rgba(67, 97, 238, 0.1);
  border-radius: 20px;
  color: var(--primary);
  text-decoration: none;
  font-size: 0.9rem;
  font-weight: 600;
  transition: all 0.3s ease;
}

.project-link i {
  margin-right: 8px;
}

.project-link:hover {
  background-color: var(--primary);
  color: var(--text);
  transform: translateY(-3px);
}

@media (max-width: 768px) {
  .project-card {
    padding: 20px;
  }
  
  .project-title {
    font-size: 1.4rem;
  }
  
  .project-links {
    flex-direction: column;
    gap: 10px;
  }
}
</style>