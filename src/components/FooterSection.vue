<template>
    <footer class="footer-section">
        <div class="container">
            <div class="footer-content">
                <div class="footer-info">
                    <h3>聯絡資訊</h3>
                    <div class="contact-info">
                        <p>Email: sakuei@gmail.com</p>
                    </div>
                </div>
                
                <div class="footer-social">
                    <h3>社群媒體</h3>
                    <div class="social-links">
                        <a href="https://github.com/sakueinozomi" class="social-link">GitHub</a>
                        <a href="https://tw.linkedin.com/in/lucille-chiang-52a21516b" class="social-link">LinkedIn</a>
                    </div>
                </div>
                
                <div class="footer-links">
                    <h3>快速連結</h3>
                    <nav class="footer-nav">
                        <a href="#info">關於我</a>
                        <a href="#skills">技能</a>
                        <a href="#projects">專案</a>
                        <a href="#experience">經歷</a>
                    </nav>
                </div>
            </div>
            
            <div class="footer-bottom">
                <p>&copy; 2025 個人簡報. All rights reserved.</p>
            </div>
        </div>
    </footer>
</template>

<script setup>
// Footer 組件邏輯
</script>

<style lang="scss" scoped>
.footer-section {
    background: linear-gradient(135deg, var(--bg-dark) 0%, #1a1a2e 100%);
    color: var(--text-light);
    min-height: 40vh;
    width: 100vw;
    padding: 3rem 0;
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
    
    .footer-content {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
        gap: 3rem;
        margin-bottom: 2rem;
        
        .footer-info,
        .footer-social,
        .footer-links {
            text-align: center;
            
            h3 {
                color: var(--primary-color);
                margin-bottom: 1.5rem;
                font-size: 1.4rem;
                font-weight: 600;
            }
        }
        
        .contact-info {
            p {
                margin-bottom: 0.8rem;
                color: rgba(255, 255, 255, 0.85);
                font-size: 1.05rem;
            }
        }
        
        .social-links {
            display: flex;
            gap: 1.2rem;
            justify-content: center;
            
            .social-link {
                color: rgba(255, 255, 255, 0.8);
                text-decoration: none;
                padding: 0.8rem 1.5rem;
                border: 2px solid rgba(255, 255, 255, 0.3);
                border-radius: 8px;
                transition: all 0.3s ease;
                font-weight: 500;
                
                &:hover {
                    color: var(--primary-color);
                    border-color: var(--primary-color);
                    transform: translateY(-3px);
                    box-shadow: 0 5px 15px rgba(100, 108, 255, 0.3);
                }
            }
        }
        
        .footer-nav {
            display: flex;
            flex-direction: column;
            gap: 0.8rem;
            align-items: center;
            
            a {
                color: rgba(255, 255, 255, 0.8);
                text-decoration: none;
                transition: color 0.3s ease;
                font-size: 1.05rem;
                
                &:hover {
                    color: var(--primary-color);
                }
            }
        }
    }
    
    .footer-bottom {
        border-top: 1px solid rgba(255, 255, 255, 0.15);
        padding-top: 2rem;
        text-align: center;
        
        p {
            color: rgba(255, 255, 255, 0.6);
            margin: 0;
            font-size: 1rem;
        }
    }
}

@media (max-width: 768px) {
    .footer-section {
        .footer-content {
            grid-template-columns: 1fr;
            gap: 2rem;
            
            .social-links {
                flex-direction: column;
                align-items: center;
                
                .social-link {
                    width: 200px;
                }
            }
        }
    }
}
</style>
