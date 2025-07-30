<template>
    <section id="projects" class="project-section">
        <div class="container">
            <h2 class="section-title">專案作品</h2>
            <div class="project-slider">
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
                            :style="{ transform: `translateX(-${currentSlide * 85}%)` }"
                        >
                            <div 
                                class="project-card" 
                                v-for="project in projects" 
                                :key="project.id"
                            >
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
                    
                    <button 
                        class="slider-btn next-btn" 
                        @click="nextSlide"
                        :disabled="currentSlide === projects.length - 1"
                    >
                        ›
                    </button>
                </div>
                
                <div class="slide-indicators">
                    <span 
                        v-for="(project, index) in projects" 
                        :key="project.id"
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
import { ref, onMounted, onUnmounted } from 'vue'

const currentSlide = ref(0)
const sliderContainer = ref(null)
let startX = 0
let isDragging = false

const baseUrl = import.meta.env.BASE_URL

const projects = ref([
    {
        id: 1,
        title: '專案名稱 1',
        description: '這是一個示例專案的描述',
        image: `${baseUrl}sample/sample-1.png`,
        technologies: ['Vue.js', 'SCSS', 'JavaScript']
    },
    {
        id: 2,
        title: '專案名稱 2',
        description: '這是另一個示例專案的描述',
        image: `${baseUrl}sample/sample-2.png`,
        technologies: ['Vue.js', 'TypeScript', 'Vite']
    },
    {
        id: 3,
        title: '專案名稱 3',
        description: '這是另一個示例專案的描述',
        image: `${baseUrl}sample/sample-3.png`,
        technologies: ['Vue.js', 'TypeScript', 'Vite']
    }
])

const nextSlide = () => {
    if (currentSlide.value < projects.value.length - 1) {
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
    
    .project-slider {
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
                    
                    .project-card {
                        flex: 0 0 85%;
                        margin-right: 2rem;
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
                            height: 400px;
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

@media (max-width: 768px) {
    .project-section {
        .section-title {
            font-size: 2.5rem;
        }
        
        .project-slider {
            .slider-wrapper {
                .slider-btn {
                    width: 40px;
                    font-size: 1.2rem;
                    
                    &.prev-btn {
                        margin-right: 0.5rem;
                    }
                    
                    &.next-btn {
                        margin-left: 0.5rem;
                    }
                }
                
                .slider-container {
                    .slider-track {
                        .project-card {
                            flex: 0 0 90%;
                            margin-right: 1rem;
                            
                            .project-image {
                                height: 180px;
                            }
                            
                            .project-content {
                                padding: 1.5rem;
                                
                                h3 {
                                    font-size: 1.4rem;
                                }
                                
                                p {
                                    font-size: 1rem;
                                }
                                
                                .project-tech {
                                    gap: 0.4rem;
                                    
                                    .tech-tag {
                                        font-size: 0.8rem;
                                        padding: 0.3rem 0.8rem;
                                    }
                                }
                            }
                        }
                    }
                }
            }
            
            .slide-indicators {
                gap: 0.5rem;
                
                .indicator {
                    width: 10px;
                    height: 10px;
                }
            }
        }
    }
}
</style>
