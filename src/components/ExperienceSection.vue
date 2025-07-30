<template>
  <section class="experience-section">
    <div class="container">
      <h2 class="section-title">工作經歷</h2>
      <div class="timeline">
        <div class="timeline-item" v-for="experience in experiences" :key="experience.id">
          <div class="timeline-marker"></div>
          <div class="timeline-content">
            <div class="timeline-period">{{ experience.period }}</div>
            <h3>{{ experience.position }}</h3>
            <h4>{{ experience.company }}</h4>
            <p>{{ experience.description }}</p>
            <ul class="responsibilities">
              <li v-for="responsibility in experience.responsibilities" :key="responsibility">
                {{ responsibility }}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const experiences = ref([
  {
    id: 1,
    period: '2023 - 現在',
    position: '前端工程師',
    company: '科技公司 A',
    description: '負責前端開發與使用者體驗優化',
    responsibilities: [
      '開發響應式網頁應用程式',
      '維護現有系統功能',
      '與團隊協作完成專案'
    ]
  },
  {
    id: 2,
    period: '2021 - 2023',
    position: '初級前端工程師',
    company: '科技公司 B',
    description: '學習前端技術並參與專案開發',
    responsibilities: [
      '學習 Vue.js 框架',
      '協助完成網頁功能開發',
      '參與程式碼審查'
    ]
  }
])
</script>

<style lang="scss" scoped>
.experience-section {
  padding: 4rem 0;
  background-color: var(--bg-secondary);
  
  .container {
    max-width: 1000px;
    margin: 0 auto;
    padding: 0 2rem;
  }
  
  .section-title {
    text-align: center;
    margin-bottom: 3rem;
    font-size: 2.5rem;
    color: var(--text-color);
  }
  
  .timeline {
    position: relative;
    
    &::before {
      content: '';
      position: absolute;
      left: 20px;
      top: 0;
      bottom: 0;
      width: 2px;
      background-color: var(--primary-color);
    }
    
    .timeline-item {
      position: relative;
      margin-bottom: 3rem;
      padding-left: 60px;
      
      .timeline-marker {
        position: absolute;
        left: 11px;
        top: 0;
        width: 18px;
        height: 18px;
        background-color: var(--primary-color);
        border-radius: 50%;
        border: 3px solid var(--bg-secondary);
      }
      
      .timeline-content {
        background-color: var(--card-bg);
        padding: 2rem;
        border-radius: 8px;
        box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        
        .timeline-period {
          color: var(--primary-color);
          font-weight: 600;
          font-size: 0.9rem;
          margin-bottom: 0.5rem;
        }
        
        h3 {
          color: var(--text-color);
          margin-bottom: 0.5rem;
          font-size: 1.4rem;
        }
        
        h4 {
          color: var(--text-secondary);
          margin-bottom: 1rem;
          font-weight: 500;
        }
        
        p {
          color: var(--text-secondary);
          line-height: 1.6;
          margin-bottom: 1.5rem;
        }
        
        .responsibilities {
          list-style: none;
          padding: 0;
          
          li {
            position: relative;
            padding-left: 1.5rem;
            margin-bottom: 0.5rem;
            color: var(--text-secondary);
            
            &::before {
              content: '•';
              position: absolute;
              left: 0;
              color: var(--primary-color);
              font-weight: bold;
            }
          }
        }
      }
    }
  }
}
</style>
