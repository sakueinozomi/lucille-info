<template>
    <section id="skills" class="skill-section">
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
        name: 'Vue2/Vue3',
        description: '現代前端框架開發'
    },
    {
        name: 'Nuxt2/Nuxt3',
        description: 'SEO友好的Vue.js框架'
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
    min-height: 100vh;
    width: 100vw;
    padding: 0;
    background-color: var(--bg-secondary);
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
    
    .skills-grid {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        gap: 2.5rem;
        
        .skill-item {
            padding: 2.5rem;
            background-color: var(--card-bg);
            border-radius: 12px;
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            text-align: center;
            
            &:hover {
                transform: translateY(-8px);
                box-shadow: 0 8px 30px rgba(0, 0, 0, 0.15);
            }
            
            h3 {
                margin-bottom: 1.5rem;
                color: var(--primary-color);
                font-size: 1.5rem;
                font-weight: 600;
            }
            
            p {
                color: var(--text-secondary);
                line-height: 1.6;
                font-size: 1.1rem;
            }
        }
    }
}

@media (max-width: 768px) {
    .skill-section {
        .section-title {
            font-size: 2.5rem;
        }
        
        .skills-grid {
            grid-template-columns: 1fr;
            gap: 1.5rem;
            
            .skill-item {
                padding: 2rem;
				cursor: pointer;
            }
        }
    }
}
</style>
