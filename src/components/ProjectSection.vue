<template>
  <section class="project-section">
    <div class="container">
      <h2 class="section-title">專案作品</h2>
      <div class="projects-grid">
        <div class="project-card" v-for="project in projects" :key="project.id">
          <div class="project-image">
            <img :src="project.image" :alt="project.title" />
          </div>
          <div class="project-content">
            <h3>{{ project.title }}</h3>
            <p>{{ project.description }}</p>
            <div class="project-tech">
              <span v-for="tech in project.technologies" :key="tech" class="tech-tag">
                {{ tech }}
              </span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const projects = ref([
  {
    id: 1,
    title: '專案名稱 1',
    description: '這是一個示例專案的描述',
    image: '/src/assets/sample/sample-1.png',
    technologies: ['Vue.js', 'SCSS', 'JavaScript']
  },
  {
    id: 2,
    title: '專案名稱 2',
    description: '這是另一個示例專案的描述',
    image: '/src/assets/sample/sample-2.png',
    technologies: ['Vue.js', 'TypeScript', 'Vite']
  }
])
</script>

<style lang="scss" scoped>
.project-section {
  padding: 4rem 0;
  background-color: var(--bg-color);
  
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
  
  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 2rem;
    
    .project-card {
      background-color: var(--card-bg);
      border-radius: 12px;
      overflow: hidden;
      box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      
      &:hover {
        transform: translateY(-8px);
        box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
      }
      
      .project-image {
        width: 100%;
        height: 200px;
        overflow: hidden;
        
        img {
          width: 100%;
          height: 100%;
          object-fit: cover;
          transition: transform 0.3s ease;
        }
        
        &:hover img {
          transform: scale(1.05);
        }
      }
      
      .project-content {
        padding: 1.5rem;
        
        h3 {
          margin-bottom: 1rem;
          color: var(--text-color);
          font-size: 1.4rem;
        }
        
        p {
          color: var(--text-secondary);
          line-height: 1.6;
          margin-bottom: 1.5rem;
        }
        
        .project-tech {
          display: flex;
          flex-wrap: wrap;
          gap: 0.5rem;
          
          .tech-tag {
            background-color: var(--primary-color);
            color: white;
            padding: 0.3rem 0.8rem;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 500;
          }
        }
      }
    }
  }
}
</style>
