<template>
  <footer class="footer-section">
    <div class="container">
      <div class="footer-content">
        <div class="footer-info">
          <h3>聯絡資訊</h3>
          <div class="contact-info">
            <p>Email: example@email.com</p>
            <p>電話: +886 123 456 789</p>
          </div>
        </div>
        
        <div class="footer-social">
          <h3>社群媒體</h3>
          <div class="social-links">
            <a href="#" class="social-link">GitHub</a>
            <a href="#" class="social-link">LinkedIn</a>
            <a href="#" class="social-link">Twitter</a>
          </div>
        </div>
        
        <div class="footer-links">
          <h3>快速連結</h3>
          <nav class="footer-nav">
            <a href="#info">關於我</a>
            <a href="#skills">技能</a>
            <a href="#projects">專案</a>
            <a href="#experience">經歷</a>
          </nav>
        </div>
      </div>
      
      <div class="footer-bottom">
        <p>&copy; 2025 個人作品集. All rights reserved.</p>
      </div>
    </div>
  </footer>
</template>

<script setup>
// Footer 組件邏輯
</script>

<style lang="scss" scoped>
.footer-section {
  background-color: var(--bg-dark);
  color: var(--text-light);
  padding: 3rem 0 1rem;
  
  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 2rem;
  }
  
  .footer-content {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2rem;
    margin-bottom: 2rem;
    
    .footer-info,
    .footer-social,
    .footer-links {
      h3 {
        color: var(--primary-color);
        margin-bottom: 1rem;
        font-size: 1.2rem;
      }
    }
    
    .contact-info {
      p {
        margin-bottom: 0.5rem;
        color: rgba(255, 255, 255, 0.8);
      }
    }
    
    .social-links {
      display: flex;
      gap: 1rem;
      
      .social-link {
        color: rgba(255, 255, 255, 0.8);
        text-decoration: none;
        padding: 0.5rem 1rem;
        border: 1px solid rgba(255, 255, 255, 0.3);
        border-radius: 4px;
        transition: all 0.3s ease;
        
        &:hover {
          color: var(--primary-color);
          border-color: var(--primary-color);
          transform: translateY(-2px);
        }
      }
    }
    
    .footer-nav {
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
      
      a {
        color: rgba(255, 255, 255, 0.8);
        text-decoration: none;
        transition: color 0.3s ease;
        
        &:hover {
          color: var(--primary-color);
        }
      }
    }
  }
  
  .footer-bottom {
    border-top: 1px solid rgba(255, 255, 255, 0.1);
    padding-top: 1rem;
    text-align: center;
    
    p {
      color: rgba(255, 255, 255, 0.6);
      margin: 0;
    }
  }
}

@media (max-width: 768px) {
  .footer-content {
    grid-template-columns: 1fr;
    text-align: center;
    
    .social-links {
      justify-content: center;
    }
  }
}
</style>
