<template>
    <footer class="footer">
      <div class="container footer-container">
        <div class="footer-content">
          <div class="footer-left">
            <div class="footer-logo">
              <span class="logo-text">A<span class="highlight">S</span></span>
            </div>
            <p class="footer-tagline">Software Engineer | Problem Solver | Tech Enthusiast</p>
          </div>
          
          <div class="footer-nav">
            <h4>Quick Links</h4>
            <ul>
              <li><a href="#about">About</a></li>
              <li><a href="#experience">Experience</a></li>
              <li><a href="#projects">Projects</a></li>
              <li><a href="#skills">Skills</a></li>
              <li><a href="#contact">Contact</a></li>
            </ul>
          </div>
          
          <div class="footer-social">
            <h4>Connect</h4>
            <div class="social-icons">
              <a href="https://www.linkedin.com/in/agampreet-singh1/" target="_blank">
                <i class="fab fa-linkedin-in"></i>
              </a>
              <a href="https://www.instagram.com/agam0802/" target="_blank">
                <i class="fab fa-instagram"></i>
              </a>
              <a href="https://discord.com/users/agam7" target="_blank">
                <i class="fab fa-discord"></i>
              </a>
              <a href="https://github.com/agam7777" target="_blank">
                <i class="fab fa-github"></i>
              </a>
              <a href="mailto:agampreet.singh2003@gmail.com">
                <i class="fas fa-envelope"></i>
              </a>
            </div>
          </div>
        </div>
        
        <div class="footer-bottom">
          <div class="copyright">
            &copy; {{ currentYear }} Agampreet Singh. All rights reserved.
          </div>
          
          <div class="scroll-top" @click="scrollToTop">
            <i class="fas fa-arrow-up"></i>
          </div>
        </div>
      </div>
    </footer>
  </template>
  
  <script>
  export default {
    name: 'FooterSection',
    data() {
      return {
        currentYear: new Date().getFullYear(),
      }
    },
    methods: {
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
  .footer {
    background-color: var(--surface);
    padding: 60px 0 20px;
    position: relative;
  }
  
  .footer-container {
    display: flex;
    flex-direction: column;
  }
  
  .footer-content {
    display: grid;
    grid-template-columns: 2fr 1fr 1fr;
    gap: 40px;
    margin-bottom: 40px;
  }
  
  .footer-left {
    display: flex;
    flex-direction: column;
  }
  
  .footer-logo {
    margin-bottom: 15px;
  }
  
  .logo-text {
    font-size: 2rem;
    font-weight: 700;
    color: var(--text);
  }
  
  .highlight {
    color: var(--primary);
  }
  
  .footer-tagline {
    font-size: 1rem;
    color: var(--text-secondary);
    line-height: 1.5;
  }
  
  .footer-nav h4, .footer-social h4 {
    font-size: 1.1rem;
    margin-bottom: 20px;
    position: relative;
    display: inline-block;
  }
  
  .footer-nav h4::after, .footer-social h4::after {
    content: '';
    position: absolute;
    width: 30px;
    height: 2px;
    background-color: var(--primary);
    bottom: -8px;
    left: 0;
  }
  
  .footer-nav ul {
    list-style: none;
    padding: 0;
  }
  
  .footer-nav ul li {
    margin-bottom: 10px;
  }
  
  .footer-nav ul li a {
    color: var(--text-secondary);
    text-decoration: none;
    transition: color 0.3s ease;
    display: inline-block;
    position: relative;
  }
  
  .footer-nav ul li a::after {
    content: '';
    position: absolute;
    width: 0;
    height: 1px;
    bottom: -2px;
    left: 0;
    background-color: var(--primary);
    transition: width 0.3s ease;
  }
  
  .footer-nav ul li a:hover {
    color: var(--primary);
  }
  
  .footer-nav ul li a:hover::after {
    width: 100%;
  }
  
  .social-icons {
    display: flex;
    gap: 15px;
  }
  
  .social-icons a {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 40px;
    height: 40px;
    background-color: rgba(67, 97, 238, 0.1);
    border-radius: 50%;
    color: var(--text);
    transition: all 0.3s ease;
    border: 1px solid var(--primary);
  }
  
  .social-icons a:hover {
    background-color: var(--primary);
    color: white;
    transform: translateY(-5px);
  }
  
  .footer-bottom {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding-top: 20px;
    border-top: 1px solid rgba(255, 255, 255, 0.1);
  }
  
  .copyright {
    font-size: 0.9rem;
    color: var(--text-secondary);
  }
  
  .scroll-top {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: var(--primary);
    display: flex;
    justify-content: center;
    align-items: center;
    color: white;
    cursor: pointer;
    transition: all 0.3s ease;
  }
  
  .scroll-top:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
  }
  
  @media (max-width: 768px) {
    .footer-content {
      grid-template-columns: 1fr;
      gap: 30px;
      text-align: center;
    }
    
    .footer-nav h4::after, .footer-social h4::after {
      left: 50%;
      transform: translateX(-50%);
    }
    
    .social-icons {
      justify-content: center;
    }
    
    .footer-bottom {
      flex-direction: column;
      gap: 20px;
    }
  }
  </style>