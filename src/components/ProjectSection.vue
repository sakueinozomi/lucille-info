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
                            :style="{ 
                                transform: `translateX(-${currentSlide * (100 / projects.length)}%)`,
                                width: `${projects.length * 100}%`
                            }"
                        >
                            <div 
                                class="project-card" 
                                v-for="project in projects" 
                                :key="project.id"
                                @click="handleCardClick(project)"
                                :class="{ 'clickable': true }"
                                :style="cardStyle"
                            >
                                <div class="project-card-inner">
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
        
        <!-- Lightbox -->
        <div v-if="lightboxOpen" class="lightbox-overlay" @click="closeLightbox">
            <div class="lightbox-container" @click.stop>
                <button class="lightbox-close" @click="closeLightbox">×</button>
                <div class="lightbox-content">
                    <div class="lightbox-header">
                        <h3>{{ currentProject.title }}</h3>
                        <p>{{ currentLightboxImageIndex + 1 }} / {{ currentProject.images?.length || 0 }}</p>
                    </div>
                    <div class="lightbox-image-container">
                        <button 
                            class="lightbox-nav prev" 
                            @click="prevLightboxImage"
                            :disabled="currentLightboxImageIndex === 0"
                        >‹</button>
                        <img 
                            :src="currentProject.images?.[currentLightboxImageIndex]" 
                            :alt="`${currentProject.title} - 圖片 ${currentLightboxImageIndex + 1}`"
                            class="lightbox-image"
                        />
                        <button 
                            class="lightbox-nav next" 
                            @click="nextLightboxImage"
                            :disabled="currentLightboxImageIndex === (currentProject.images?.length || 1) - 1"
                        >›</button>
                    </div>
                    <div class="lightbox-thumbnails">
                        <img 
                            v-for="(image, index) in currentProject.images" 
                            :key="index"
                            :src="image" 
                            :alt="`縮圖 ${index + 1}`"
                            class="lightbox-thumbnail"
                            :class="{ active: index === currentLightboxImageIndex }"
                            @click="currentLightboxImageIndex = index"
                        />
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue'

const currentSlide = ref(0)
const sliderContainer = ref(null)
const lightboxOpen = ref(false)
const currentProject = ref({})
const currentLightboxImageIndex = ref(0)
let startX = 0
let isDragging = false

const baseUrl = import.meta.env.BASE_URL

// 計算卡片寬度
const cardStyle = computed(() => {
    const totalProjects = projects.value.length
    // 每張卡片佔據 slider-track 總寬度的 1/totalProjects
    return {
        width: `${100 / totalProjects}%`
    }
})

const projects = ref([
    {
        id: 1,
        title: 'PIXNET 首頁',
        description: '痞客邦全新首頁，翻新 10 年老頁面，規劃並使用 Nuxt2 和 Vuex 實現前後端分離，提升 SEO 與使用者體驗。',
        image: `${baseUrl}sample/sample-5.png`,
        technologies: ['Nuxt2', 'SCSS', 'JavaScript'],
        type: 'site',
        url: 'https://www.pixnet.net/'
    },
    {
        id: 2,
        title: 'Array APV 後台前端',
        description: 'Array APV 後台前端系統，使用 Vue3 與 Pinia 進行開發。',
        image: `${baseUrl}sample/sample-2.png`,
        technologies: ['Vue3', 'Pinia', 'UI/UX'],
        type: 'image',
        images: [
            `${baseUrl}sample/sample-2.png`,
            `${baseUrl}sample/sample-3.png`,
            `${baseUrl}sample/sample-4.png`,
            `${baseUrl}sample/sample-1.png`
        ]
    },
    {
        id: 3,
        title: '阿卡學院官網',
        description: '接案前端官網，使用 Nuxt3 與 Vite 進行開發。',
        image: `${baseUrl}sample/sample-6.png`,
        technologies: ['Nuxt3', 'Vite'],
        type: 'site',
        url: 'https://drop-point-server-dev22.zeabur.app'
    },
	{
        id: 4,
        title: 'PIXNET 活動網站',
        description: '公司合作接案之前端活動網站，使用 Vue3 與 Vuex 進行開發。',
        image: `${baseUrl}sample/sample-7.png`,
        technologies: ['Vue3', 'Vuex'],
        type: 'site',
        url: 'https://2023carrefour-ricedumpling.events.pixnet.net/'
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

// 處理卡片點擊
const handleCardClick = (project) => {
    if (project.type === 'site' && project.url) {
        window.open(project.url, '_blank')
    } else if (project.type === 'image' && project.images) {
        openLightbox(project)
    }
}

// Lightbox 功能
const openLightbox = (project) => {
    currentProject.value = project
    currentLightboxImageIndex.value = 0
    lightboxOpen.value = true
    document.body.style.overflow = 'hidden'
}

const closeLightbox = () => {
    lightboxOpen.value = false
    currentProject.value = {}
    currentLightboxImageIndex.value = 0
    document.body.style.overflow = 'auto'
}

const nextLightboxImage = () => {
    if (currentLightboxImageIndex.value < (currentProject.value.images?.length || 0) - 1) {
        currentLightboxImageIndex.value++
    }
}

const prevLightboxImage = () => {
    if (currentLightboxImageIndex.value > 0) {
        currentLightboxImageIndex.value--
    }
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
    // 確保在組件卸載時恢復 body overflow
    document.body.style.overflow = 'auto'
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
                    
                    .project-card {
                        flex-shrink: 0;
                        background-color: transparent;
                        cursor: pointer;
                        padding: 0 1rem;
                        box-sizing: border-box;
                        
                        .project-card-inner {
                            background-color: var(--card-bg);
                            border-radius: 16px;
                            overflow: hidden;
                            box-shadow: 0 6px 25px rgba(0, 0, 0, 0.1);
                            transition: transform 0.3s ease, box-shadow 0.3s ease;
                            height: 100%;
                        }
                        
                        &.clickable:hover .project-card-inner {
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
                                margin-bottom: 1rem;
                                
                                .tech-tag {
                                    background-color: var(--primary-color);
                                    color: white;
                                    border: 1px solid var(--primary-color);
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

// Lightbox 樣式
.lightbox-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.9);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000;
    animation: fadeIn 0.3s ease;
    
    .lightbox-container {
        position: relative;
        max-width: 90vw;
        max-height: 90vh;
        background: rgba(0, 0, 0, 0.7);
        border-radius: 12px;
        overflow: hidden;
        animation: slideUp 0.3s ease;
        
        .lightbox-close {
            position: absolute;
            top: 15px;
            right: 15px;
            background: rgba(0, 0, 0, 0.7);
            color: #fff;
            border: none;
            width: 35px;
            height: 35px;
            border-radius: 50%;
            font-size: 1.5rem;
            cursor: pointer;
            z-index: 10;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: background 0.3s ease;
            
            &:hover {
                background: rgba(0, 0, 0, 0.9);
            }
        }
        
        .lightbox-content {
            .lightbox-header {
                padding: 1.5rem;
                background: var(--card-bg);
                border-bottom: 1px solid rgba(0, 0, 0, 0.1);
                display: flex;
                justify-content: space-between;
                align-items: center;
                
                h3 {
                    margin: 0;
                    color: var(--text-color);
                    font-size: 1.3rem;
                }
                
                p {
                    margin: 0;
                    color: var(--text-secondary);
                    font-size: 0.9rem;
                }
            }
            
            .lightbox-image-container {
                position: relative;
                background: #f5f5f5;
                display: flex;
                align-items: center;
                justify-content: center;
                min-height: 400px;
                max-height: 60vh;
                
                .lightbox-image {
                    max-width: 100%;
                    max-height: 100%;
                    object-fit: contain;
                }
                
                .lightbox-nav {
                    position: absolute;
                    top: 50%;
                    transform: translateY(-50%);
                    background: rgba(0, 0, 0, 0.7);
                    color: white;
                    border: none;
                    width: 50px;
                    height: 50px;
                    border-radius: 50%;
                    font-size: 1.5rem;
                    cursor: pointer;
                    transition: all 0.3s ease;
                    display: flex;
                    align-items: center;
                    justify-content: center;
                    
                    &:hover:not(:disabled) {
                        background: rgba(0, 0, 0, 0.9);
                        transform: translateY(-50%) scale(1.1);
                    }
                    
                    &:disabled {
                        background: rgba(0, 0, 0, 0.3);
                        cursor: not-allowed;
                    }
                    
                    &.prev {
                        left: 15px;
                    }
                    
                    &.next {
                        right: 15px;
                    }
                }
            }
            
            .lightbox-thumbnails {
                display: flex;
                gap: 0.5rem;
                padding: 1rem;
                background: var(--card-bg);
                overflow-x: auto;
                
                .lightbox-thumbnail {
                    width: 60px;
                    height: 40px;
                    object-fit: cover;
                    border-radius: 4px;
                    cursor: pointer;
                    transition: all 0.3s ease;
                    opacity: 0.6;
                    border: 2px solid transparent;
                    
                    &:hover {
                        opacity: 0.8;
                    }
                    
                    &.active {
                        opacity: 1;
                        border-color: var(--primary-color);
                    }
                }
            }
        }
    }
}

@keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
}

@keyframes slideUp {
    from { 
        opacity: 0;
        transform: translateY(30px);
    }
    to { 
        opacity: 1;
        transform: translateY(0);
    }
}
</style>
