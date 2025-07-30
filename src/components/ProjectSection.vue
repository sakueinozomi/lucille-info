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
    min-height: 100vh;
    width: 100vw;
    padding: 0;
    background-color: var(--bg-color);
    display: flex;
    align-items: center;
    justify-content: center;
    
    .container {
        max-width: 1200px;
        width: 100%;
        margin: 0 auto;
        padding: 0 2rem;
        display: flex;
        flex-direction: column;
        justify-content: center;
        height: 100%;
    }
    
    .section-title {
        text-align: center;
        margin-bottom: 4rem;
        font-size: 3.5rem;
        color: var(--text-color);
        font-weight: 700;
    }
    
    .projects-grid {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
        gap: 3rem;
        
        .project-card {
            background-color: var(--card-bg);
            border-radius: 16px;
            overflow: hidden;
            box-shadow: 0 6px 25px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            
            &:hover {
                transform: translateY(-10px);
                box-shadow: 0 12px 40px rgba(0, 0, 0, 0.2);
            }
            
            .project-image {
                width: 100%;
                height: 220px;
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
                padding: 2rem;
                
                h3 {
                    margin-bottom: 1.2rem;
                    color: var(--text-color);
                    font-size: 1.6rem;
                    font-weight: 600;
                }
                
                p {
                    color: var(--text-secondary);
                    line-height: 1.7;
                    margin-bottom: 1.8rem;
                    font-size: 1.05rem;
                }
                
                .project-tech {
                    display: flex;
                    flex-wrap: wrap;
                    gap: 0.6rem;
                    
                    .tech-tag {
                        background-color: var(--primary-color);
                        color: white;
                        padding: 0.4rem 1rem;
                        border-radius: 25px;
                        font-size: 0.85rem;
                        font-weight: 500;
                    }
                }
            }
        }
    }
}

@media (max-width: 768px) {
    .project-section {
        .section-title {
            font-size: 2.5rem;
        }
        
        .projects-grid {
            grid-template-columns: 1fr;
            gap: 2rem;
            
            .project-card {
                .project-content {
                    padding: 1.5rem;
                }
            }
        }
    }
}
</style>
