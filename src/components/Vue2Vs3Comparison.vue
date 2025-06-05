<template>
    <div class="vue2-vs-vue3-main">
        <div class="header">
            <h1>🚀 Vue 2 vs Vue 3 語法對比</h1>
            <p>完整的語法轉換指南 - 從 Options API 到 Composition API</p>
        </div>

        <div class="navigation-cards">
            <!-- 學習導覽 -->
            <div class="nav-card intro-card" @click="showComponent = 'index'">
                <div class="card-icon">📚</div>
                <h3>學習導覽</h3>
                <p>了解學習路徑、快速參考和重點提示</p>
                <div class="card-badge">推薦先看</div>
            </div>

            <!-- 完整對比演示 -->
            <div class="nav-card demo-card" @click="showComponent = 'demo'">
                <div class="card-icon">⚡</div>
                <h3>完整語法對比</h3>
                <p>詳細的語法對比與實際操作演示</p>
                <div class="card-badge">核心內容</div>
            </div>
        </div>

        <!-- 快速語法對照 -->
        <div class="quick-syntax-section">
            <h2>🔥 最常用語法快速對照</h2>
            <div class="syntax-grid">
                <div class="syntax-card">
                    <h4>響應式數據</h4>
                    <div class="syntax-comparison">
                        <div class="vue2-syntax">
                            <span class="version-label">Vue 2</span>
                            <code>data() { return { count: 0 } }</code>
                        </div>
                        <div class="arrow">→</div>
                        <div class="vue3-syntax">
                            <span class="version-label">Vue 3</span>
                            <code>const count = ref(0)</code>
                        </div>
                    </div>
                </div>

                <div class="syntax-card">
                    <h4>計算屬性</h4>
                    <div class="syntax-comparison">
                        <div class="vue2-syntax">
                            <span class="version-label">Vue 2</span>
                            <code>computed: { fullName() {...} }</code>
                        </div>
                        <div class="arrow">→</div>
                        <div class="vue3-syntax">
                            <span class="version-label">Vue 3</span>
                            <code>const fullName = computed(...)</code>
                        </div>
                    </div>
                </div>

                <div class="syntax-card">
                    <h4>生命週期</h4>
                    <div class="syntax-comparison">
                        <div class="vue2-syntax">
                            <span class="version-label">Vue 2</span>
                            <code>mounted() { console.log('mounted') }</code>
                        </div>
                        <div class="arrow">→</div>
                        <div class="vue3-syntax">
                            <span class="version-label">Vue 3</span>
                            <code>onMounted(() => {...})</code>
                        </div>
                    </div>
                </div>

                <div class="syntax-card">
                    <h4>方法定義</h4>
                    <div class="syntax-comparison">
                        <div class="vue2-syntax">
                            <span class="version-label">Vue 2</span>
                            <code>methods: { handleClick() {...} }</code>
                        </div>
                        <div class="arrow">→</div>
                        <div class="vue3-syntax">
                            <span class="version-label">Vue 3</span>
                            <code>const handleClick = () => {...}</code>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- 動態顯示組件 -->
        <div v-if="showComponent" class="component-container">
            <div class="component-header">
                <button @click="showComponent = null" class="back-btn">← 返回</button>
                <h2>{{ componentTitle }}</h2>
            </div>

            <component :is="currentComponent" />
        </div>

        <!-- 學習提示 -->
        <div v-if="!showComponent" class="learning-tips">
            <h2>💡 學習小提示</h2>
            <div class="tips-grid">
                <div class="tip-card">
                    <div class="tip-icon">🎯</div>
                    <h4>循序漸進</h4>
                    <p>建議先看「學習導覽」了解整體架構，再進入「完整語法對比」</p>
                </div>
                <div class="tip-card">
                    <div class="tip-icon">💻</div>
                    <h4>動手實作</h4>
                    <p>每個演示都可以實際操作，記得多多實驗不同的輸入值</p>
                </div>
                <div class="tip-card">
                    <div class="tip-icon">📝</div>
                    <h4>做筆記</h4>
                    <p>將重要的語法差異記錄下來，建立自己的轉換參考手冊</p>
                </div>
                <div class="tip-card">
                    <div class="tip-icon">🔄</div>
                    <h4>反覆練習</h4>
                    <p>語法轉換需要時間適應，多練習幾次就會變得自然</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import Vue2Vs3ComparisonIndex from './Vue2Vs3Comparison/Vue2Vs3ComparisonIndex.vue'
import Vue2Vs3ComparisonDemo from './Vue2Vs3Comparison/Vue2Vs3ComparisonDemo.vue'

const showComponent = ref(null)

const currentComponent = computed(() => {
    switch (showComponent.value) {
        case 'index':
            return Vue2Vs3ComparisonIndex
        case 'demo':
            return Vue2Vs3ComparisonDemo
        default:
            return null
    }
})

const componentTitle = computed(() => {
    switch (showComponent.value) {
        case 'index':
            return '學習導覽與快速參考'
        case 'demo':
            return '完整語法對比演示'
        default:
            return ''
    }
})
</script>

<style scoped>
.vue2-vs-vue3-main {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.header {
    text-align: center;
    margin-bottom: 3rem;
    padding: 3rem 2rem;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    border-radius: 20px;
    color: white;
    box-shadow: 0 10px 30px rgba(102, 126, 234, 0.3);
}

.header h1 {
    font-size: 3rem;
    margin-bottom: 1rem;
    font-weight: 700;
    text-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.header p {
    font-size: 1.3rem;
    opacity: 0.9;
    margin: 0;
}

.navigation-cards {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 2rem;
    margin-bottom: 4rem;
}

.nav-card {
    background: white;
    border-radius: 16px;
    padding: 2.5rem;
    text-align: center;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
    position: relative;
    overflow: hidden;
}

.nav-card:hover {
    transform: translateY(-8px);
    box-shadow: 0 12px 40px rgba(0, 0, 0, 0.15);
}

.intro-card {
    border-left: 5px solid #4CAF50;
}

.intro-card:hover {
    background: linear-gradient(135deg, #4CAF50, #45a049);
    color: white;
}

.demo-card {
    border-left: 5px solid #2196F3;
}

.demo-card:hover {
    background: linear-gradient(135deg, #2196F3, #1976D2);
    color: white;
}

.card-icon {
    font-size: 3rem;
    margin-bottom: 1rem;
}

.nav-card h3 {
    font-size: 1.5rem;
    margin-bottom: 1rem;
    color: #2c3e50;
}

.nav-card:hover h3 {
    color: white;
}

.nav-card p {
    color: #666;
    line-height: 1.6;
    margin-bottom: 1.5rem;
}

.nav-card:hover p {
    color: rgba(255, 255, 255, 0.9);
}

.card-badge {
    background: #FF9800;
    color: white;
    padding: 0.4rem 1rem;
    border-radius: 20px;
    font-size: 0.8rem;
    font-weight: 600;
    display: inline-block;
}

.quick-syntax-section {
    background: #f8f9fa;
    padding: 3rem;
    border-radius: 20px;
    margin-bottom: 4rem;
}

.quick-syntax-section h2 {
    text-align: center;
    color: #2c3e50;
    margin-bottom: 2rem;
    font-size: 2rem;
}

.syntax-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.5rem;
}

.syntax-card {
    background: white;
    border-radius: 12px;
    padding: 1.5rem;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.syntax-card h4 {
    color: #2c3e50;
    margin-bottom: 1rem;
    font-size: 1.1rem;
}

.syntax-comparison {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    flex-wrap: wrap;
}

.vue2-syntax,
.vue3-syntax {
    display: flex;
    flex-direction: column;
    align-items: center;
    flex: 1;
    min-width: 120px;
}

.version-label {
    font-size: 0.7rem;
    font-weight: 600;
    margin-bottom: 0.3rem;
    text-transform: uppercase;
}

.vue2-syntax .version-label {
    color: #e74c3c;
}

.vue3-syntax .version-label {
    color: #27ae60;
}

.syntax-comparison code {
    background: #f4f4f4;
    padding: 0.4rem 0.6rem;
    border-radius: 6px;
    font-size: 0.8rem;
    font-family: 'Courier New', monospace;
    text-align: center;
    word-break: break-all;
}

.arrow {
    color: #666;
    font-weight: bold;
    margin: 0 0.5rem;
}

.component-container {
    margin-top: 2rem;
}

.component-header {
    display: flex;
    align-items: center;
    gap: 1rem;
    margin-bottom: 2rem;
    padding-bottom: 1rem;
    border-bottom: 2px solid #eee;
}

.back-btn {
    background: #6c757d;
    color: white;
    border: none;
    padding: 0.5rem 1rem;
    border-radius: 8px;
    cursor: pointer;
    font-size: 0.9rem;
    transition: background 0.3s ease;
}

.back-btn:hover {
    background: #5a6268;
}

.component-header h2 {
    color: #2c3e50;
    margin: 0;
}

.learning-tips {
    background: linear-gradient(135deg, #fff3cd, #ffeaa7);
    padding: 3rem;
    border-radius: 20px;
    border-left: 5px solid #ffc107;
}

.learning-tips h2 {
    text-align: center;
    color: #856404;
    margin-bottom: 2rem;
    font-size: 2rem;
}

.tips-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1.5rem;
}

.tip-card {
    background: white;
    padding: 1.5rem;
    border-radius: 12px;
    text-align: center;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.tip-icon {
    font-size: 2rem;
    margin-bottom: 1rem;
}

.tip-card h4 {
    color: #2c3e50;
    margin-bottom: 0.5rem;
}

.tip-card p {
    color: #666;
    font-size: 0.9rem;
    line-height: 1.5;
}

@media (max-width: 768px) {
    .vue2-vs-vue3-main {
        padding: 1rem;
    }

    .header h1 {
        font-size: 2rem;
    }

    .navigation-cards {
        grid-template-columns: 1fr;
    }

    .syntax-grid {
        grid-template-columns: 1fr;
    }

    .tips-grid {
        grid-template-columns: 1fr;
    }

    .syntax-comparison {
        flex-direction: column;
        gap: 1rem;
    }

    .arrow {
        transform: rotate(90deg);
    }
}
</style>
