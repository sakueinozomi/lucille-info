<template>
  <section class="skill-section">
    <div class="container">
      <h2 class="section-title">技能專長</h2>
      <div class="skills-grid">
        <div class="skill-item" v-for="skill in skills" :key="skill.name">
          <h3>{{ skill.name }}</h3>
          <p>{{ skill.description }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const skills = ref([
  {
    name: 'Vue.js',
    description: '現代前端框架開發'
  },
  {
    name: 'JavaScript',
    description: '核心程式語言技能'
  },
  {
    name: 'SCSS',
    description: '進階樣式處理'
  }
])
</script>

<style lang="scss" scoped>
.skill-section {
  padding: 4rem 0;
  background-color: var(--bg-secondary);
  
  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 2rem;
  }
  
  .section-title {
    text-align: center;
    margin-bottom: 3rem;
    font-size: 2.5rem;
    color: var(--text-color);
  }
  
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
    
    .skill-item {
      padding: 2rem;
      background-color: var(--card-bg);
      border-radius: 8px;
      box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
      transition: transform 0.3s ease;
      
      &:hover {
        transform: translateY(-5px);
      }
      
      h3 {
        margin-bottom: 1rem;
        color: var(--primary-color);
        font-size: 1.3rem;
      }
      
      p {
        color: var(--text-secondary);
        line-height: 1.6;
      }
    }
  }
}
</style>
