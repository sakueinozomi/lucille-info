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
    min-height: 100vh;
    width: 100vw;
    padding: 0;
    background-color: var(--bg-secondary);
    display: flex;
    align-items: center;
    justify-content: center;
    
    .container {
        max-width: 1000px;
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
    
    .timeline {
        position: relative;
        max-height: 60vh;
        overflow-y: auto;
        padding-right: 1rem;
        
        &::-webkit-scrollbar {
            width: 6px;
        }
        
        &::-webkit-scrollbar-track {
            background: var(--bg-secondary);
        }
        
        &::-webkit-scrollbar-thumb {
            background: var(--primary-color);
            border-radius: 3px;
        }
        
        &::before {
            content: '';
            position: absolute;
            left: 20px;
            top: 0;
            bottom: 0;
            width: 3px;
            background-color: var(--primary-color);
        }
        
        .timeline-item {
            position: relative;
            margin-bottom: 3rem;
            padding-left: 60px;
            
            .timeline-marker {
                position: absolute;
                left: 9px;
                top: 0;
                width: 22px;
                height: 22px;
                background-color: var(--primary-color);
                border-radius: 50%;
                border: 4px solid var(--bg-secondary);
                z-index: 1;
            }
            
            .timeline-content {
                background-color: var(--card-bg);
                padding: 2.5rem;
                border-radius: 12px;
                box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
                transition: transform 0.3s ease, box-shadow 0.3s ease;
                
                &:hover {
                    transform: translateX(10px);
                    box-shadow: 0 8px 30px rgba(0, 0, 0, 0.15);
                }
                
                .timeline-period {
                    color: var(--primary-color);
                    font-weight: 700;
                    font-size: 1rem;
                    margin-bottom: 0.8rem;
                    text-transform: uppercase;
                    letter-spacing: 0.5px;
                }
                
                h3 {
                    color: var(--text-color);
                    margin-bottom: 0.5rem;
                    font-size: 1.6rem;
                    font-weight: 600;
                }
                
                h4 {
                    color: var(--text-secondary);
                    margin-bottom: 1.2rem;
                    font-weight: 500;
                    font-size: 1.1rem;
                }
                
                p {
                    color: var(--text-secondary);
                    line-height: 1.7;
                    margin-bottom: 1.8rem;
                    font-size: 1.05rem;
                }
                
                .responsibilities {
                    list-style: none;
                    padding: 0;
                    
                    li {
                        position: relative;
                        padding-left: 1.8rem;
                        margin-bottom: 0.8rem;
                        color: var(--text-secondary);
                        line-height: 1.6;
                        
                        &::before {
                            content: '▸';
                            position: absolute;
                            left: 0;
                            color: var(--primary-color);
                            font-weight: bold;
                            font-size: 1.1rem;
                        }
                    }
                }
            }
        }
    }
}

@media (max-width: 768px) {
    .experience-section {
        .section-title {
            font-size: 2.5rem;
        }
        
        .timeline {
            max-height: 70vh;
            
            .timeline-item {
                .timeline-content {
                    padding: 2rem;
                    
                    &:hover {
                        transform: translateX(5px);
                    }
                }
            }
        }
    }
}
</style>
