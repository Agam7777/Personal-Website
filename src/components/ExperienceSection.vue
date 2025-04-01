<template>
  <section id="experience" class="section experience-section">
    <div class="container">
      <h2 class="section-title">Professional Experience</h2>
      
      <div class="timeline">
        <div class="timeline-item" v-for="(job, index) in jobs" :key="index">
          <div class="timeline-dot" :style="{ backgroundColor: job.color }"></div>
          <div class="timeline-content card glow">
            <div class="job-header">
              <div class="header-with-logo">
                <div class="company-logo-container">
                  <img :src="job.logoPath" :alt="job.company + ' logo'" class="company-logo" />
                </div>
                <div class="header-content">
                  <h3>{{ job.title }}</h3>
                  <div class="company-info">
                    <span class="company-name">{{ job.company }}</span>
                    <span class="separator">|</span>
                    <span class="job-location">{{ job.location }}</span>
                  </div>
                  <div class="job-duration">{{ job.duration }}</div>
                </div>
              </div>
            </div>
            
            <ul class="job-responsibilities">
              <li v-for="(resp, respIndex) in job.responsibilities" :key="respIndex">
                {{ resp }}
              </li>
            </ul>
            
            <div class="job-tech" v-if="job.technologies && job.technologies.length > 0">
              <span class="tech-label">Technologies:</span>
              <div class="tech-tags">
                <span v-for="(tech, techIndex) in job.technologies" :key="techIndex" class="tech-tag">
                  {{ tech }}
                </span>
              </div>
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
  name: 'ExperienceSection',
  setup() {
    gsap.registerPlugin(ScrollTrigger);
    
    const jobs = ref([
      {
        title: 'Software Development Engineer Intern',
        company: 'Expedia Group',
        location: 'Seattle, WA',
        duration: 'June 2024 – August 2024',
        color: '#4361ee',
        logoPath: '/images/expedia_group.png',
        responsibilities: [
          'Developed a key feature to display and manage marketing feed cards, enhancing the admin tool for the marketing team by integrating Java-based services with Spring and MongoDB for seamless data retrieval and updates.',
          'Utilized Amazon S3 buckets for efficient storage and retrieval of large datasets, streamlining data management processes.',
          'Deployed code to production using Spinnaker for continuous delivery, ensuring smooth and automated deployment workflows.',
          'Built and maintained RESTful APIs for backend-frontend communication and employed GraphQL for data fetching, ensuring responsive UI development using React and TypeScript.',
          'Implemented Jest mock testing for the frontend to ensure robust, reliable code quality before deployment.',
          'Used Jira to track tasks and manage progress throughout the project lifecycle, contributing to timely feature completion.',
          'Collaborated in an Agile environment, participating in daily scrum meetings and iterative development cycles to incorporate regular stakeholder feedback, leading to the successful deployment of the project to production.'
        ],
        technologies: ['Java', 'Spring', 'MongoDB', 'Amazon S3', 'React', 'TypeScript', 'GraphQL', 'Jest', 'Spinnaker', 'Jira']
      },
      {
        title: 'Product Specialist (Part-Time)',
        company: 'Apple',
        location: 'Seattle, WA',
        duration: 'August 2022 – August 2023',
        color: '#7209b7',
        logoPath: '/images/apple.png',
        responsibilities: [
          'Diagnosed and resolved technical issues on customers\' devices by analyzing unique situations and providing effective troubleshooting solutions.',
          'Engaged with customers seeking new products, delivering comprehensive product knowledge, and assisting in choosing the ideal Apple products tailored to their needs.',
          'Effectively introduced and promoted Apple\'s business solutions to customers, aligning them with relevant contexts and benefits.'
        ],
        technologies: ['Technical Support', 'Customer Service', 'Product Knowledge', 'Troubleshooting']
      }
    ]);
    
    onMounted(() => {
      animateTimeline();
      animateLogos();
    });
    
    const animateTimeline = () => {
      gsap.from('.timeline-item', {
        scrollTrigger: {
          trigger: '.experience-section',
          start: 'top 70%',
        },
        opacity: 0,
        y: 50,
        stagger: 0.2,
        duration: 0.8,
        ease: 'power2.out'
      });
    };

    const animateLogos = () => {
      gsap.from('.company-logo', {
        scrollTrigger: {
          trigger: '.experience-section',
          start: 'top 70%',
        },
        scale: 0.5,
        opacity: 0,
        duration: 1,
        ease: 'elastic.out(1, 0.5)',
        stagger: 0.3
      });
    };
    
    return {
      jobs
    };
  }
}
</script>

<style scoped>
.experience-section {
  background-color: var(--background);
}

.timeline {
  position: relative;
  max-width: 1000px;
  margin: 0 auto;
}

.timeline::before {
  content: '';
  position: absolute;
  width: 2px;
  background: linear-gradient(to bottom, var(--primary), var(--accent));
  top: 0;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
}

.timeline-item {
  padding: 10px 40px;
  position: relative;
  width: 50%;
  box-sizing: border-box;
  margin-bottom: 30px;
}

.timeline-item:nth-child(odd) {
  left: 0;
}

.timeline-item:nth-child(even) {
  left: 50%;
}

.timeline-dot {
  position: absolute;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  right: -10px;
  top: 15px;
  z-index: 10;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
}

.timeline-item:nth-child(even) .timeline-dot {
  left: -10px;
}

.timeline-content {
  padding: 20px;
  border-radius: 10px;
  position: relative;
  overflow: hidden;
}

.header-with-logo {
  display: flex;
  align-items: flex-start;
  position: relative;
  margin-bottom: 5px;
}

.company-logo-container {
  flex-shrink: 0;
  width: 60px;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 15px;
  border-radius: 8px;
  background-color: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(5px);
  overflow: hidden;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  position: relative;
}

.company-logo {
  max-width: 85%;
  max-height: 85%;
  object-fit: contain;
  transition: transform 0.3s ease;
}

.company-logo-container:hover .company-logo {
  transform: scale(1.1);
}

.header-content {
  flex-grow: 1;
}

.job-header {
  margin-bottom: 15px;
}

.job-header h3 {
  color: var(--primary);
  font-size: 1.3rem;
  margin-bottom: 8px;
  margin-top: 0;
}

.company-info {
  display: flex;
  align-items: center;
  font-size: 1.1rem;
  margin-bottom: 5px;
}

.company-name {
  font-weight: 600;
}

.separator {
  margin: 0 10px;
  color: var(--text-secondary);
}

.job-duration {
  color: var(--text-secondary);
  font-size: 0.9rem;
}

.job-responsibilities {
  list-style-type: none;
  padding: 0;
  margin: 15px 0;
}

.job-responsibilities li {
  position: relative;
  padding-left: 20px;
  margin-bottom: 10px;
  line-height: 1.5;
}

.job-responsibilities li::before {
  content: '→';
  position: absolute;
  left: 0;
  color: var(--primary);
  font-weight: bold;
}

.job-tech {
  margin-top: 15px;
  display: flex;
  flex-direction: column;
}

.tech-label {
  font-weight: 600;
  margin-bottom: 8px;
  color: var(--text-secondary);
}

.tech-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.tech-tag {
  padding: 5px 10px;
  background-color: rgba(67, 97, 238, 0.1);
  border-radius: 20px;
  font-size: 0.8rem;
  border: 1px solid var(--primary);
  white-space: nowrap;
}

@media (max-width: 768px) {
  .timeline::before {
    left: 30px;
  }
  
  .timeline-item {
    width: 100%;
    padding-left: 70px;
    padding-right: 0;
  }
  
  .timeline-item:nth-child(even) {
    left: 0;
  }
  
  .timeline-dot {
    left: 20px;
    right: auto;
  }
  
  .timeline-item:nth-child(even) .timeline-dot {
    left: 20px;
  }

  .header-with-logo {
    flex-direction: column;
  }

  .company-logo-container {
    width: 50px;
    height: 50px;
    margin-bottom: 10px;
    align-self: flex-start;
  }
}
</style>