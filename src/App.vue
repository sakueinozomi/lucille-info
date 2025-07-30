<script setup>
import InfoSection from './components/InfoSection.vue'
import SkillSection from './components/SkillSection.vue'
import ProjectSection from './components/ProjectSection.vue'
import ExperienceSection from './components/ExperienceSection.vue'
import FooterSection from './components/FooterSection.vue'
</script>

<template>
    <div id="app">
        <InfoSection />
        <SkillSection />
        <ProjectSection />
        <ExperienceSection />
        <FooterSection />
    </div>
</template>

<style lang="scss" scoped>
#app {
    min-height: 100vh;
    width: 100%;
    margin: 0;
    padding: 0;
    text-align: left;
}

// 為每個 section 加入基礎樣式
:deep(.info-section),
:deep(.skill-section),
:deep(.project-section),
:deep(.experience-section) {
    min-height: 100vh;
    width: 100vw;
    scroll-snap-align: start;
    display: flex;
    align-items: center;
    justify-content: center;
}

:deep(.footer-section) {
    min-height: 40vh;
    width: 100vw;
    scroll-snap-align: start;
}

// CSS 變數定義
:root {
    --primary-color: #646cff;
    --primary-hover: #535bf2;
    --bg-color: #ffffff;
    --bg-secondary: #f8f9fa;
    --bg-dark: #242424;
    --text-color: #213547;
    --text-secondary: #666;
    --text-light: rgba(255, 255, 255, 0.87);
    --card-bg: #ffffff;
}

@media (prefers-color-scheme: dark) {
    :root {
        --bg-color: #1a1a1a;
        --bg-secondary: #242424;
        --text-color: rgba(255, 255, 255, 0.87);
        --text-secondary: rgba(255, 255, 255, 0.7);
        --card-bg: #2a2a2a;
    }
}
</style>
