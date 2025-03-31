<template>
  <section id="contact" class="section contact-section">
    <div class="container">
      <h2 class="section-title">Get In Touch</h2>
      
      <div class="contact-content">
        <div class="contact-info card glow">
          <h3>Let's Connect</h3>
          <p>I'm currently looking for new opportunities. Whether you have a question or just want to say hi, I'll try my best to get back to you!</p>
          
          <div class="contact-methods">
            <div class="contact-method">
              <div class="method-icon">
                <i class="fas fa-envelope"></i>
              </div>
              <div class="method-details">
                <h4>Email</h4>
                <a href="mailto:agampreet.singh2003@gmail.com">agampreet.singh2003@gmail.com</a>
              </div>
            </div>

            <div class="contact-method">
              <div class="method-icon">
                <i class="fas fa-phone"></i>
              </div>
              <div class="method-details">
                <h4>Phone</h4>
                <a href="tel:+14255983133">+1 (425)-598-3133</a>
              </div>
            </div>
            
            <div class="contact-method">
              <div class="method-icon">
                <i class="fab fa-linkedin-in"></i>
              </div>
              <div class="method-details">
                <h4>LinkedIn</h4>
                <a href="https://www.linkedin.com/in/agampreet-singh1/" target="_blank">@agampreet-singh1</a>
              </div>
            </div>

            <div class="contact-method">
              <div class="method-icon">
                <i class="fab fa-discord"></i>
              </div>
              <div class="method-details">
                <h4>Discord</h4>
                <a href="https://discord.com/users/agam7" target="_blank">@agam7</a>
              </div>
            </div>

            <div class="contact-method">
              <div class="method-icon">
                <i class="fab fa-instagram"></i>
              </div>
              <div class="method-details">
                <h4>Discord</h4>
                <a href="https://www.instagram.com/agam0802/" target="_blank">@agam0802</a>
              </div>
            </div>
          </div>
        </div>
        
        <div class="contact-form card glow">
          <h3>Send a Message</h3>
          <form @submit.prevent="submitForm" ref="form">
            <div class="form-group">
              <label for="name">Name</label>
              <input 
                type="text" 
                id="name" 
                name="name"
                v-model="formData.name" 
                placeholder="Your Name" 
                required
              />
            </div>
            
            <div class="form-group">
              <label for="email">Email</label>
              <input 
                type="email" 
                id="email" 
                name="email"
                v-model="formData.email" 
                placeholder="Your Email" 
                required
              />
            </div>
            
            <div class="form-group">
              <label for="subject">Subject</label>
              <input 
                type="text" 
                id="subject" 
                name="subject"
                v-model="formData.subject" 
                placeholder="Subject" 
                required
              />
            </div>
            
            <div class="form-group">
              <label for="message">Message</label>
              <textarea 
                id="message" 
                name="message"
                v-model="formData.message" 
                placeholder="Your Message" 
                required
                rows="5"
              ></textarea>
            </div>
            
            <button type="submit" class="submit-btn" :disabled="isSubmitting">
              <span v-if="!isSubmitting">Send Message</span>
              <span v-else><i class="fas fa-spinner fa-spin"></i> Sending...</span>
            </button>
            
            <div v-if="formStatus.message" :class="['form-status', formStatus.type]">
              {{ formStatus.message }}
            </div>
          </form>
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
  name: 'ContactSection',
  setup() {
    gsap.registerPlugin(ScrollTrigger);
    
    const form = ref(null);
    const formData = ref({
      name: '',
      email: '',
      subject: '',
      message: ''
    });
    
    const isSubmitting = ref(false);
    const formStatus = ref({
      message: '',
      type: ''
    });
    
    const emailjsConfig = {
      serviceID: 'service_ntrr6sb', 
      templateID: 'template_r8ica24',
    };
    
    const submitForm = async () => {
      if (!window.emailjs) {
        formStatus.value = {
          message: 'EmailJS not loaded. Please refresh the page and try again.',
          type: 'error'
        };
        return;
      }
      
      isSubmitting.value = true;
      formStatus.value = { message: '', type: '' };
      
      try {
        await window.emailjs.sendForm(
          emailjsConfig.serviceID,
          emailjsConfig.templateID,
          form.value
        );
        
        // Success message
        formStatus.value = {
          message: 'Message sent successfully! I\'ll get back to you soon.',
          type: 'success'
        };
        
        formData.value = {
          name: '',
          email: '',
          subject: '',
          message: ''
        };
      } catch (error) {
        console.error('Error sending email:', error);
        
        // Error message
        formStatus.value = {
          message: 'Oops! Something went wrong. Please try again later.',
          type: 'error'
        };
      } finally {
        isSubmitting.value = false;
      }
    };
    
    onMounted(() => {
      animateElements();
    });
    
    const animateElements = () => {
      gsap.from('.contact-info', {
        scrollTrigger: {
          trigger: '.contact-section',
          start: 'top 70%',
        },
        x: -50,
        opacity: 0,
        duration: 0.8,
        ease: 'power2.out'
      });
      
      gsap.from('.contact-form', {
        scrollTrigger: {
          trigger: '.contact-section',
          start: 'top 70%',
        },
        x: 50,
        opacity: 0,
        duration: 0.8,
        ease: 'power2.out'
      });
    };
    
    return {
      form,
      formData,
      isSubmitting,
      formStatus,
      submitForm
    };
  }
}
</script>

<style scoped>
.contact-section {
  background-color: var(--surface-light);
  position: relative;
}

.contact-content {
  display: grid;
  grid-template-columns: 1fr 1.5fr;
  gap: 40px;
}

.contact-info, .contact-form {
  padding: 30px;
}

.contact-info h3, .contact-form h3 {
  font-size: 1.5rem;
  margin-bottom: 20px;
  color: var(--primary);
}

.contact-info p {
  margin-bottom: 30px;
  line-height: 1.6;
  color: var(--text-secondary);
}

.contact-methods {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.contact-method {
  display: flex;
  align-items: center;
  gap: 20px;
}

.method-icon {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background: linear-gradient(45deg, var(--primary), var(--accent));
  display: flex;
  justify-content: center;
  align-items: center;
}

.method-icon i {
  color: white;
  font-size: 1.2rem;
}

.method-details h4 {
  font-size: 1.1rem;
  margin-bottom: 5px;
}

.method-details a {
  color: var(--text-secondary);
  text-decoration: none;
  transition: color 0.3s ease;
}

.method-details a:hover {
  color: var(--primary);
}

.form-group {
  margin-bottom: 20px;
}

.form-group label {
  display: block;
  margin-bottom: 8px;
  font-weight: 500;
}

.form-group input, .form-group textarea {
  width: 100%;
  padding: 12px 15px;
  background-color: var(--surface);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 8px;
  color: var(--text);
  font-family: inherit;
  transition: border-color 0.3s ease;
}

.form-group input:focus, .form-group textarea:focus {
  outline: none;
  border-color: var(--primary);
}

.form-group textarea {
  resize: vertical;
  min-height: 120px;
}

.submit-btn {
  display: inline-block;
  padding: 12px 25px;
  background: linear-gradient(45deg, var(--primary), var(--accent));
  color: white;
  border: none;
  border-radius: 8px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.submit-btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
}

.submit-btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
  transform: none;
}

.form-status {
  margin-top: 15px;
  padding: 10px;
  border-radius: 5px;
  font-size: 0.9rem;
}

.form-status.success {
  background-color: rgba(39, 174, 96, 0.1);
  color: #27ae60;
  border: 1px solid #27ae60;
}

.form-status.error {
  background-color: rgba(231, 76, 60, 0.1);
  color: #e74c3c;
  border: 1px solid #e74c3c;
}

@media (max-width: 992px) {
  .contact-content {
    grid-template-columns: 1fr;
  }
  
  .contact-info, .contact-form {
    max-width: 600px;
    margin: 0 auto;
  }
}

@media (max-width: 576px) {
  .contact-method {
    flex-direction: column;
    align-items: flex-start;
    gap: 10px;
  }
  
  .method-details {
    text-align: center;
    width: 100%;
  }
}
</style>