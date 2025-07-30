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
  padding: 4rem 0;
  background-color: var(--bg-color);
  
  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 2rem;
  }
  
  .section-title {
    text-align: center;
    margin-bottom: 2rem;
    font-size: 2.5rem;
    color: var(--text-color);
  }
  
  .info-content {
    display: flex;
    justify-content: center;
    align-items: center;
    
    .info-text {
      font-size: 1.1rem;
      line-height: 1.6;
      color: var(--text-secondary);
    }
  }
}
</style>
