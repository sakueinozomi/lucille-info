<template>
    <section id="info" class="info-section">
        <div class="container">
            <h2 class="section-title">關於我</h2>
            <div class="info-content">
                <div class="info-text">
                    <p>
						江尹瑄 | Lucille Chiang
					</p>
					<p>
						Front-End Developer | Vue Ecosystem Enthusiast
					</p>
					<p>
						6 年以上前端開發經驗，使用 Vue/Nuxt 架構，進行前端系統重構、與跨國團隊協作。
					</p>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
</script>

<style lang="scss" scoped>
.info-section {
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
        align-items: center;
        height: 100%;
    }
    
    .section-title {
        text-align: center;
        margin-bottom: 3rem;
        font-size: 3.5rem;
        color: var(--text-color);
        font-weight: 700;
    }
    
    .info-content {
        display: flex;
        justify-content: center;
        align-items: center;
        max-width: 800px;
        
        .info-text {
            font-size: 1.3rem;
            line-height: 1.8;
            color: var(--text-secondary);
            text-align: center;
        }
    }
}
</style>
