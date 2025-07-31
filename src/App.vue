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
        <ExperienceSection />
        <SkillSection />
        <ProjectSection />
        <FooterSection />
        <div class="screen-size-warning">
            <div class="warning-icon">�</div>
            <div class="warning-title">請使用桌機或筆電觀看</div>
            <div class="warning-message">
                此為簡報用途設計<br>
                建議使用桌機或筆電瀏覽以獲得最佳體驗
            </div>
        </div>
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
</style>
