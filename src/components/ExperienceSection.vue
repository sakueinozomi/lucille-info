<template>
    <section id="experience" class="experience-section">
        <div class="container">
            <h2 class="section-title">工作經歷</h2>
            <div class="experience-slider">
                <div class="slider-wrapper">
                    <button 
                        class="slider-btn prev-btn" 
                        @click="prevSlide" 
                        :disabled="currentSlide === 0"
                    >
                        ‹
                    </button>
                    
                    <div class="slider-container" ref="sliderContainer">
                        <div 
                            class="slider-track" 
                            :style="{ 
                                transform: `translateX(-${currentSlide * (100 / experiences.length)}%)`,
                                width: `${experiences.length * 100}%`
                            }"
                        >
                            <div 
                                class="experience-card" 
                                v-for="experience in experiences" 
                                :key="experience.id"
                                :style="cardStyle"
                            >
                                <div class="experience-card-inner">
                                    <div class="card-header">
                                        <div class="timeline-period">{{ experience.period }}</div>
                                    </div>
                                    <div class="card-content">
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
                    </div>
                    
                    <button 
                        class="slider-btn next-btn" 
                        @click="nextSlide"
                        :disabled="currentSlide === experiences.length - 1"
                    >
                        ›
                    </button>
                </div>
                
                <div class="slide-indicators">
                    <span 
                        v-for="(experience, index) in experiences" 
                        :key="experience.id"
                        class="indicator"
                        :class="{ active: index === currentSlide }"
                        @click="goToSlide(index)"
                    ></span>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue'

const currentSlide = ref(0)
const sliderContainer = ref(null)
let startX = 0
let isDragging = false

// 計算卡片寬度
const cardStyle = computed(() => {
    const totalExperiences = experiences.value.length
    return {
        width: `${100 / totalExperiences}%`
    }
})

const experiences = ref([
    {
        id: 1,
        period: '2024 - 現在',
        position: '前端工程師',
        company: '美商安瑞(ARRAY NETWORKS)',
        description: '負責後台系統之前端開發',
        responsibilities: [
            '新產品架構設計,使用Vue 3、Pinia、vue-router，導入新版Element Plus與 ECharts，實現前後端分離並改善維運效率。',
            '在舊系統中使用Vue 2、jQuery維護現有系統功能，並持續在既有專案中增加新功能並維護。',
            '維護舊專案之PHP前端頁面。'
        ]
    },
    {
        id: 2,
        period: '2022 - 2024',
        position: '前端工程師',
        company: 'PIXNET(城邦集團)',
        description: '與後端團隊協作，並使用Nuxt2開發全新痞客邦首頁。',
        responsibilities: [
            '使用Nuxt2與各式套件進行前端頁面開發，以提升頁面SEO與翻新首頁畫面。',
            '使用Vue2/Vue3進行活動頁面開發。',
			'串接GA/MC等追蹤工具以蒐集使用者行為數據。'
        ]
    },
	{
        id: 3,
        period: '2018 - 2022',
        position: '前端工程師',
        company: '美商網碩(FriendFinder Network)',
        description: '開發前端直播系統與登陸頁面',
        responsibilities: [
            '使用Angular8進行直播系統開發。',
            '使用jQuery與原生JS建構登陸頁面。',
			'串接Hotjar，協助統計team收集使用者行為點擊數據。'
        ]
    },
	{
        id: 4,
        period: '2017 - 2018',
        position: 'PHP後端工程師',
        company: '橙色數位',
        description: '開發議程系統頁面',
        responsibilities: [
            '使用Angularjs進行議程系統頁面的前台與後台開發。',
            '利用jQuery串接API協作前端功能。',
			'PHP後端開發，使用CI框架進行資料庫操作。'
        ]
    },
])

const nextSlide = () => {
    if (currentSlide.value < experiences.value.length - 1) {
        currentSlide.value++
    }
}

const prevSlide = () => {
    if (currentSlide.value > 0) {
        currentSlide.value--
    }
}

const goToSlide = (index) => {
    currentSlide.value = index
}

// 觸控滑動支援
const handleTouchStart = (e) => {
    startX = e.touches[0].clientX
    isDragging = true
}

const handleTouchMove = (e) => {
    if (!isDragging) return
    e.preventDefault()
}

const handleTouchEnd = (e) => {
    if (!isDragging) return
    isDragging = false
    
    const endX = e.changedTouches[0].clientX
    const diffX = startX - endX
    const threshold = 50
    
    if (Math.abs(diffX) > threshold) {
        if (diffX > 0) {
            nextSlide()
        } else {
            prevSlide()
        }
    }
}

onMounted(() => {
    if (sliderContainer.value) {
        sliderContainer.value.addEventListener('touchstart', handleTouchStart, { passive: true })
        sliderContainer.value.addEventListener('touchmove', handleTouchMove, { passive: false })
        sliderContainer.value.addEventListener('touchend', handleTouchEnd, { passive: true })
    }
})

onUnmounted(() => {
    if (sliderContainer.value) {
        sliderContainer.value.removeEventListener('touchstart', handleTouchStart)
        sliderContainer.value.removeEventListener('touchmove', handleTouchMove)
        sliderContainer.value.removeEventListener('touchend', handleTouchEnd)
    }
})
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
    
    .experience-slider {
        width: 100%;
        position: relative;
        
        .slider-wrapper {
            position: relative;
            display: flex;
            align-items: center;
            margin-bottom: 2rem;
            
            .slider-btn {
                background: rgba(239, 239, 239, 0.9);
                color: #333333;
                border: none;
                font-weight: 600;
                width: 50px;
                height: 50px;
                border-radius: 50%;
                font-size: 1.5rem;
                cursor: pointer;
                transition: all 0.3s ease;
                display: flex;
                align-items: center;
                justify-content: center;
                z-index: 10;
                box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
                flex-shrink: 0;
                outline: none;
                
                &.prev-btn {
                    margin-right: 1rem;
                }
                
                &.next-btn {
                    margin-left: 1rem;
                }
                
                &:hover:not(:disabled) {
                    background: rgba(239, 239, 239, 1);
                    transform: scale(1.1);
                    box-shadow: 0 6px 20px rgba(0, 0, 0, 0.2);
                }
                
                &:disabled {
                    background: rgba(239, 239, 239, 0.3);
                    color: rgba(51, 51, 51, 0.3);
                    cursor: not-allowed;
                    transform: none;
                    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
                }
            }
            
            .slider-container {
                overflow: hidden;
                width: 100%;
                position: relative;
                flex: 1;
                
                .slider-track {
                    display: flex;
                    transition: transform 0.5s cubic-bezier(0.25, 0.46, 0.45, 0.94);
                    width: 100%;
                    
                    .experience-card {
                        flex-shrink: 0;
                        padding: 0 1rem;
                        box-sizing: border-box;
                        
                        .experience-card-inner {
                            background-color: var(--card-bg);
                            border-radius: 16px;
                            box-shadow: 0 6px 30px rgba(0, 0, 0, 0.1);
                            transition: transform 0.3s ease, box-shadow 0.3s ease;
                            overflow: hidden;
                            height: 100%;
                        }
                        
                        &:hover .experience-card-inner {
                            transform: translateY(-8px);
                            box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
                        }
                        
                        .card-header {
                            background: linear-gradient(135deg, var(--primary-color) 0%, var(--primary-hover) 100%);
                            padding: 2rem;
                            position: relative;
                            color: white;
                            
                            .timeline-period {
                                font-weight: 700;
                                font-size: 1.1rem;
                                text-transform: uppercase;
                                letter-spacing: 1px;
                                margin: 0;
                            }
                            
                            .timeline-marker {
                                position: absolute;
                                top: 50%;
                                right: 2rem;
                                transform: translateY(-50%);
                                width: 20px;
                                height: 20px;
                                background-color: rgba(255, 255, 255, 0.3);
                                border: 3px solid white;
                                border-radius: 50%;
                            }
                        }
                        
                        .card-content {
                            padding: 2.5rem;
                            
                            h3 {
                                color: var(--text-color);
                                margin-bottom: 0.8rem;
                                font-size: 1.8rem;
                                font-weight: 600;
                            }
                            
                            h4 {
                                color: var(--text-secondary);
                                margin-bottom: 1.5rem;
                                font-weight: 500;
                                font-size: 1.2rem;
                            }
                            
                            p {
                                color: var(--text-secondary);
                                line-height: 1.7;
                                margin-bottom: 2rem;
                                font-size: 1.1rem;
                            }
                            
                            .responsibilities {
                                list-style: none;
                                padding: 0;
                                
                                li {
                                    position: relative;
                                    padding-left: 2rem;
                                    margin-bottom: 1rem;
                                    color: var(--text-secondary);
                                    line-height: 1.6;
                                    font-size: 1.05rem;
                                    
                                    &::before {
                                        content: '▸';
                                        position: absolute;
                                        left: 0;
                                        color: var(--primary-color);
                                        font-weight: bold;
                                        font-size: 1.2rem;
                                    }
                                }
                            }
                        }
                    }
                }
            }
        }
        
        .slide-indicators {
            display: flex;
            justify-content: center;
            gap: 0.8rem;
            
            .indicator {
                width: 12px;
                height: 12px;
                border-radius: 50%;
                background: rgba(239, 239, 239, 0.3);
                cursor: pointer;
                transition: all 0.3s ease;
                
                &.active {
                    background: rgba(239, 239, 239, 0.7);
                    transform: scale(1.2);
                }
                
                &:hover {
                    background: rgba(239, 239, 239, 0.7);
                }
            }
        }
    }
}
</style>
