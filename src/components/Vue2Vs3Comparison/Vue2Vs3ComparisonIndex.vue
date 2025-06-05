<template>
  <div class="vue2-vs-vue3-index">
    <div class="header">
      <h1>Vue 2 vs Vue 3 語法對比學習</h1>
      <p class="subtitle">📚 從 Options API 到 Composition API 的完整轉換指南</p>
      <p class="route-info">📍 路徑：/Vue2Vs3Comparison/Vue2Vs3ComparisonIndex.vue</p>
    </div>

    <div class="learning-path">
      <h2>🎯 學習路徑</h2>
      <div class="path-grid">
        <!-- 完整對比演示 -->
        <div class="path-card main-demo">
          <div class="card-header">
            <h3>📋 完整語法對比演示</h3>
            <span class="difficulty-badge advanced">綜合</span>
          </div>
          <div class="card-content">
            <p>涵蓋所有 Vue 2 與 Vue 3 的語法差異，包含實際可操作的演示</p>
            <ul class="feature-list">
              <li>✅ 組件定義語法對比</li>
              <li>✅ 響應式數據宣告</li>
              <li>✅ 計算屬性與方法</li>
              <li>✅ 生命週期鉤子</li>
              <li>✅ 事件處理機制</li>
              <li>✅ 監聽器 (Watch)</li>
              <li>✅ 邏輯複用比較</li>
              <li>✅ 全域屬性使用</li>
            </ul>
          </div>
          <div class="card-actions">
            <button @click="navigateToFullDemo" class="btn btn-primary">
              🚀 開始完整學習
            </button>
          </div>
        </div>

        <!-- 快速參考 -->
        <div class="path-card quick-ref">
          <div class="card-header">
            <h3>⚡ 快速語法參考</h3>
            <span class="difficulty-badge beginner">入門</span>
          </div>
          <div class="card-content">
            <p>常用語法的快速對照表，適合已有基礎想快速查詢的開發者</p>
            <div class="syntax-preview">
              <div class="syntax-item">
                <span class="vue2">Vue 2: data() { return {...} }</span>
                <span class="arrow">→</span>
                <span class="vue3">Vue 3: const data = ref(...)</span>
              </div>
              <div class="syntax-item">
                <span class="vue2">Vue 2: methods: { ... }</span>
                <span class="arrow">→</span>
                <span class="vue3">Vue 3: const method = () => {...}</span>
              </div>
            </div>
          </div>
          <div class="card-actions">
            <button @click="showQuickReference" class="btn btn-secondary">
              📖 查看快速參考
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- 為什麼要學習 Vue 3 -->
    <div class="why-vue3">
      <h2>🤔 為什麼要學習 Vue 3？</h2>
      <div class="benefits-grid">
        <div class="benefit-card">
          <div class="benefit-icon">⚡</div>
          <h3>更好的性能</h3>
          <p>更小的包大小、更快的渲染速度</p>
        </div>
        <div class="benefit-card">
          <div class="benefit-icon">🔧</div>
          <h3>更好的工具支援</h3>
          <p>更強的 TypeScript 支援、更好的開發體驗</p>
        </div>
        <div class="benefit-card">
          <div class="benefit-icon">🧩</div>
          <h3>更好的邏輯複用</h3>
          <p>Composition API 讓程式碼更容易組織和複用</p>
        </div>
        <div class="benefit-card">
          <div class="benefit-icon">🚀</div>
          <h3>更現代的語法</h3>
          <p>script setup 語法糖讓開發更簡潔</p>
        </div>
      </div>
    </div>

    <!-- 快速參考摺疊區域 -->
    <div v-if="showQuickRef" class="quick-reference">
      <div class="quick-ref-header">
        <h2>⚡ 快速語法對照表</h2>
        <button @click="showQuickRef = false" class="close-btn">✕</button>
      </div>
      <div class="quick-ref-content">
        <div class="ref-section">
          <h3>1. 組件定義</h3>
          <div class="ref-comparison">
            <div class="ref-vue2">
              <h4>Vue 2</h4>
              <pre><code>export default {
  name: 'MyComponent',
  data() {
    return { count: 0 }
  },
  methods: {
    increment() {
      this.count++
    }
  }
}</code></pre>
            </div>
            <div class="ref-vue3">
              <h4>Vue 3</h4>
              <pre><code>&lt;script setup&gt;
import { ref } from 'vue'

const count = ref(0)

const increment = () => {
  count.value++
}
&lt;/script&gt;</code></pre>
            </div>
          </div>
        </div>

        <div class="ref-section">
          <h3>2. 響應式數據</h3>
          <div class="ref-comparison">
            <div class="ref-vue2">
              <pre><code>data() {
  return {
    message: 'Hello',
    user: { name: 'John' },
    items: []
  }
}</code></pre>
            </div>
            <div class="ref-vue3">
              <pre><code>const message = ref('Hello')
const user = reactive({ name: 'John' })
const items = ref([])</code></pre>
            </div>
          </div>
        </div>

        <div class="ref-section">
          <h3>3. 計算屬性</h3>
          <div class="ref-comparison">
            <div class="ref-vue2">
              <pre><code>computed: {
  fullName() {
    return this.firstName + ' ' + this.lastName
  }
}</code></pre>
            </div>
            <div class="ref-vue3">
              <pre><code>const fullName = computed(() => {
  return firstName.value + ' ' + lastName.value
})</code></pre>
            </div>
          </div>
        </div>

        <div class="ref-section">
          <h3>4. 生命週期</h3>
          <div class="ref-comparison">
            <div class="ref-vue2">
              <pre><code>created() {
  console.log('組件創建')
},
mounted() {
  console.log('組件掛載')
}</code></pre>
            </div>
            <div class="ref-vue3">
              <pre><code>// setup() 相當於 created
onMounted(() => {
  console.log('組件掛載')
})</code></pre>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- 注意事項 -->
    <div v-if="!showFullDemo" class="notes">
      <h2>💡 學習小提示</h2>
      <div class="notes-content">
        <div class="note-item">
          <span class="note-icon">📝</span>
          <div>
            <strong>逐步學習：</strong>
            不需要一次性掌握所有語法，建議先從基本的響應式數據開始
          </div>
        </div>
        <div class="note-item">
          <span class="note-icon">🔄</span>
          <div>
            <strong>實際練習：</strong>
            每個語法對比都有可操作的演示，記得動手實踐
          </div>
        </div>
        <div class="note-item">
          <span class="note-icon">📋</span>
          <div>
            <strong>保存筆記：</strong>
            建議將重要的語法差異整理成筆記，方便日後查閱
          </div>
        </div>
        <div class="note-item">
          <span class="note-icon">🤝</span>
          <div>
            <strong>漸進式遷移：</strong>
            Vue 3 向下相容 Vue 2，可以逐步遷移現有專案
          </div>
        </div>
      </div>
    </div>

    <!-- 完整演示區域 -->
    <div v-if="showFullDemo" class="full-demo-container">
      <div class="demo-header">
        <div class="demo-title">
          <h2>📋 完整語法對比演示</h2>
          <p>詳細的 Vue 2 vs Vue 3 語法對比與實際操作演示</p>
        </div>
        <button @click="hideFullDemo" class="hide-demo-btn">
          ← 返回學習導覽
        </button>
      </div>

      <div class="demo-content">
        <Vue2Vs3ComparisonDemo />
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Vue2Vs3ComparisonDemo from './Vue2Vs3ComparisonDemo.vue'

const showQuickRef = ref(false)
const showFullDemo = ref(false)

const navigateToFullDemo = () => {
  showFullDemo.value = true
  // 平滑滾動到演示區域
  setTimeout(() => {
    const demoElement = document.querySelector('.full-demo-container')
    if (demoElement) {
      demoElement.scrollIntoView({ behavior: 'smooth' })
    }
  }, 100)
}

const hideFullDemo = () => {
  showFullDemo.value = false
}

const showQuickReference = () => {
  showQuickRef.value = !showQuickRef.value
}
</script>

<style scoped>
.vue2-vs-vue3-index {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.header {
  text-align: center;
  margin-bottom: 3rem;
  padding: 2rem;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 16px;
  color: white;
}

.header h1 {
  font-size: 2.5rem;
  margin-bottom: 0.5rem;
  font-weight: 700;
}

.subtitle {
  font-size: 1.2rem;
  margin-bottom: 1rem;
  opacity: 0.9;
}

.route-info {
  background: rgba(255, 255, 255, 0.1);
  padding: 0.5rem 1rem;
  border-radius: 8px;
  font-size: 0.9rem;
  display: inline-block;
}

.learning-path {
  margin-bottom: 3rem;
}

.learning-path h2 {
  font-size: 2rem;
  margin-bottom: 1.5rem;
  color: #2c3e50;
}

.path-grid {
  display: grid;
  grid-template-columns: 2fr 1fr;
  gap: 2rem;
}

.path-card {
  background: white;
  border-radius: 16px;
  padding: 2rem;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.path-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.15);
}

.main-demo {
  border-left: 4px solid #4CAF50;
}

.quick-ref {
  border-left: 4px solid #2196F3;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
}

.card-header h3 {
  margin: 0;
  font-size: 1.4rem;
  color: #2c3e50;
}

.difficulty-badge {
  padding: 0.25rem 0.75rem;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 600;
  text-transform: uppercase;
}

.difficulty-badge.advanced {
  background: #FF9800;
  color: white;
}

.difficulty-badge.beginner {
  background: #4CAF50;
  color: white;
}

.card-content {
  margin-bottom: 1.5rem;
}

.card-content p {
  color: #666;
  line-height: 1.6;
  margin-bottom: 1rem;
}

.feature-list {
  list-style: none;
  padding: 0;
}

.feature-list li {
  margin-bottom: 0.5rem;
  color: #555;
}

.syntax-preview {
  background: #f8f9fa;
  padding: 1rem;
  border-radius: 8px;
  margin-top: 1rem;
}

.syntax-item {
  display: flex;
  align-items: center;
  margin-bottom: 0.5rem;
  font-size: 0.9rem;
}

.vue2 {
  color: #e74c3c;
  font-family: 'Courier New', monospace;
}

.vue3 {
  color: #27ae60;
  font-family: 'Courier New', monospace;
}

.arrow {
  margin: 0 0.5rem;
  color: #666;
}

.card-actions {
  text-align: center;
}

.btn {
  padding: 0.75rem 1.5rem;
  border: none;
  border-radius: 8px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-primary {
  background: #4CAF50;
  color: white;
}

.btn-primary:hover {
  background: #45a049;
  transform: translateY(-2px);
}

.btn-secondary {
  background: #2196F3;
  color: white;
}

.btn-secondary:hover {
  background: #1976D2;
  transform: translateY(-2px);
}

.why-vue3 {
  background: #f8f9fa;
  padding: 2rem;
  border-radius: 16px;
  margin-bottom: 3rem;
}

.why-vue3 h2 {
  text-align: center;
  margin-bottom: 2rem;
  color: #2c3e50;
}

.benefits-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1.5rem;
}

.benefit-card {
  background: white;
  padding: 1.5rem;
  border-radius: 12px;
  text-align: center;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.benefit-icon {
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

.benefit-card h3 {
  margin-bottom: 0.5rem;
  color: #2c3e50;
}

.benefit-card p {
  color: #666;
  font-size: 0.9rem;
}

.quick-reference {
  background: white;
  border-radius: 16px;
  padding: 2rem;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  margin-bottom: 3rem;
}

.quick-ref-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2rem;
  padding-bottom: 1rem;
  border-bottom: 2px solid #eee;
}

.close-btn {
  background: #f44336;
  color: white;
  border: none;
  border-radius: 50%;
  width: 2rem;
  height: 2rem;
  cursor: pointer;
  font-size: 1rem;
}

.ref-section {
  margin-bottom: 2rem;
}

.ref-section h3 {
  color: #2c3e50;
  margin-bottom: 1rem;
}

.ref-comparison {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
}

.ref-vue2,
.ref-vue3 {
  background: #f8f9fa;
  padding: 1rem;
  border-radius: 8px;
}

.ref-vue2 h4 {
  color: #e74c3c;
  margin-bottom: 0.5rem;
}

.ref-vue3 h4 {
  color: #27ae60;
  margin-bottom: 0.5rem;
}

.ref-vue2 pre,
.ref-vue3 pre {
  margin: 0;
  overflow-x: auto;
}

.ref-vue2 code,
.ref-vue3 code {
  font-family: 'Courier New', monospace;
  font-size: 0.9rem;
  line-height: 1.4;
}

.notes {
  background: #fff3cd;
  padding: 2rem;
  border-radius: 16px;
  border-left: 4px solid #ffc107;
}

.notes h2 {
  color: #856404;
  margin-bottom: 1.5rem;
}

.notes-content {
  display: grid;
  gap: 1rem;
}

.note-item {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
}

.note-icon {
  font-size: 1.2rem;
  flex-shrink: 0;
}

.note-item strong {
  color: #856404;
}

.full-demo-container {
  margin-top: 3rem;
  background: white;
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
}

.demo-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 2rem;
  background: linear-gradient(135deg, #4CAF50 0%, #45a049 100%);
  color: white;
}

.demo-title h2 {
  margin: 0 0 0.5rem 0;
  font-size: 1.8rem;
  font-weight: 700;
}

.demo-title p {
  margin: 0;
  opacity: 0.9;
  font-size: 1rem;
}

.hide-demo-btn {
  background: rgba(255, 255, 255, 0.2);
  color: white;
  border: 2px solid rgba(255, 255, 255, 0.3);
  padding: 0.75rem 1.5rem;
  border-radius: 8px;
  cursor: pointer;
  font-size: 0.95rem;
  font-weight: 600;
  transition: all 0.3s ease;
  white-space: nowrap;
}

.hide-demo-btn:hover {
  background: rgba(255, 255, 255, 0.3);
  border-color: rgba(255, 255, 255, 0.5);
  transform: translateY(-2px);
}

.demo-content {
  padding: 2rem;
  background: #fafafa;
}

@media (max-width: 768px) {
  .path-grid {
    grid-template-columns: 1fr;
  }

  .ref-comparison {
    grid-template-columns: 1fr;
  }

  .benefits-grid {
    grid-template-columns: 1fr;
  }

  .header h1 {
    font-size: 2rem;
  }

  .demo-header {
    flex-direction: column;
    gap: 1rem;
    text-align: center;
  }

  .demo-content {
    padding: 1rem;
  }
}
</style>
