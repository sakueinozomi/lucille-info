<template>
  <section class="info-section">
    <div class="container">
      <h2 class="section-title">關於我</h2>
      <div class="info-content">
        <div class="info-text">
          <p>這裡是個人資訊的內容區域</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
// 組件邏輯
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

@media (max-width: 768px) {
  .info-section {
    .section-title {
      font-size: 2.5rem;
    }
    
    .info-content .info-text {
      font-size: 1.1rem;
    }
  }
}
</style>
