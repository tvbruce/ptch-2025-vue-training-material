<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - Computed 計算屬性</h2>
    <p class="route-info">📍 路徑：/ComputedSamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>學習目標：</strong>透過建立簡單的商品篩選功能，掌握 computed 計算屬性的基本用法
    </p>

    <!-- 練習任務區塊 -->
    <div class="practice-tasks">
      <h3>🚀 你需要完成的練習任務</h3>
      <div class="task-grid">
        <div class="task-card">
          <div class="task-header">
            <span class="task-number">1</span>
            <h4>關鍵字搜尋</h4>
          </div>
          <div class="task-content">
            <p><strong>目標：</strong>實作 `searchedProducts` 計算屬性</p>
            <p><strong>規格：</strong></p>
            <ul>
              <li>當 `searchKeyword` 有值時，篩選出名稱包含關鍵字的商品</li>
              <li>搜尋不區分大小寫</li>
              <li>當 `searchKeyword` 為空時，回傳所有商品</li>
            </ul>
            <p><strong>提示：</strong>使用 `filter()` 和 `includes()` 方法</p>
          </div>
        </div>

        <div class="task-card">
          <div class="task-header">
            <span class="task-number">2</span>
            <h4>分類篩選</h4>
          </div>
          <div class="task-content">
            <p><strong>目標：</strong>實作 `filteredProducts` 計算屬性</p>
            <p><strong>規格：</strong></p>
            <ul>
              <li>結合關鍵字搜尋結果進行分類篩選</li>
              <li>當 `selectedCategory` 有值時，只顯示該分類的商品</li>
              <li>當 `selectedCategory` 為空時，顯示所有搜尋結果</li>
            </ul>
            <p><strong>提示：</strong>先使用 `searchedProducts` 再進行分類篩選</p>
          </div>
        </div>

        <div class="task-card">
          <div class="task-header">
            <span class="task-number">3</span>
            <h4>統計資訊</h4>
          </div>
          <div class="task-content">
            <p><strong>目標：</strong>實作統計相關的計算屬性</p>
            <p><strong>規格：</strong></p>
            <ul>
              <li>`productCount`：篩選後的商品數量</li>
              <li>`averagePrice`：篩選後商品的平均價格（取整數）</li>
            </ul>
            <p><strong>提示：</strong>使用 `reduce()` 方法計算總價，再除以數量</p>
          </div>
        </div>

        <div class="task-card">
          <div class="task-header">
            <span class="task-number">4</span>
            <h4>商品列表渲染</h4>
          </div>
          <div class="task-content">
            <p><strong>目標：</strong>在模板中渲染篩選後的商品</p>
            <p><strong>規格：</strong></p>
            <ul>
              <li>使用 `v-for` 渲染 `filteredProducts`</li>
              <li>顯示商品名稱、分類、價格</li>
              <li>當沒有符合條件的商品時，顯示提示訊息</li>
            </ul>
          </div>
        </div>
      </div>
    </div>

    <!-- 篩選介面 -->
    <div class="demo-section">
      <h3>🔍 篩選條件</h3>
      <div class="filters">
        <div class="filter-group">
          <label>🔎 搜尋商品：</label>
          <input v-model="searchKeyword" placeholder="輸入商品名稱..." class="form-input">
        </div>

        <div class="filter-group">
          <label>📂 商品分類：</label>
          <select v-model="selectedCategory" class="form-select">
            <option value="">全部分類</option>
            <option value="電子產品">電子產品</option>
            <option value="服裝">服裝</option>
            <option value="家具">家具</option>
            <option value="書籍">書籍</option>
          </select>
        </div>
      </div>
    </div>

    <!-- 統計資訊 -->
    <div class="demo-section">
      <h3>📊 統計資訊</h3>
      <div class="stats-row">
        <div class="stat-item">
          <span class="stat-label">找到商品：</span>
          <span class="stat-value">{{ productCount }} 件</span>
        </div>
        <div class="stat-item">
          <span class="stat-label">平均價格：</span>
          <span class="stat-value">${{ averagePrice }}</span>
        </div>
      </div>
    </div>

    <!-- 商品列表 -->
    <div class="demo-section">
      <h3>🛍️ 商品列表</h3>
      <div class="product-list">
        <!-- 🚀 任務4：請在這裡使用 v-for 渲染 filteredProducts -->
        <!-- 提示：記得處理空列表的情況 -->

        <!-- 暫時顯示提示，學員需要實作 v-for 渲染 -->
        <div v-if="filteredProducts.length === 0" class="no-products">
          <p>沒有找到符合條件的商品</p>
        </div>

        <!-- 學員需要在這裡添加 v-for 來渲染商品 -->
        <p class="placeholder">請完成任務4：使用 v-for 渲染 filteredProducts 中的商品</p>

        <!-- 參考格式（學員可以參考但需要自己實作）：
        <div v-for="product in filteredProducts" :key="product.id" class="product-item">
          <h4>{{ product.name }}</h4>
          <span class="category">{{ product.category }}</span>
          <p class="price">${{ product.price }}</p>
        </div>
        -->
      </div>
    </div>

    <!-- 進階提示 -->
    <div class="hint-section">
      <h4>💡 實作提示</h4>
      <details>
        <summary>📋 Computed 基本語法複習</summary>
        <pre><code>// 基本 computed 寫法
const computedProperty = computed(() => {
  // 在這裡寫計算邏輯
  return someValue
})

// 篩選範例
const filtered = computed(() => {
  return items.value.filter(item => {
    // 篩選條件
    return item.name.includes(keyword.value)
  })
})</code></pre>
      </details>

      <details>
        <summary>🔍 字串搜尋提示</summary>
        <pre><code>// 不區分大小寫搜尋
const searchResult = computed(() => {
  if (!searchKeyword.value) return products.value

  return products.value.filter(product => {
    return product.name
      .toLowerCase()
      .includes(searchKeyword.value.toLowerCase())
  })
})</code></pre>
      </details>

      <details>
        <summary>📊 統計計算提示</summary>
        <pre><code>// 計算平均值
const average = computed(() => {
  const items = filteredProducts.value
  if (items.length === 0) return 0

  const total = items.reduce((sum, item) => sum + item.price, 0)
  return Math.round(total / items.length)
})</code></pre>
      </details>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 商品資料（簡化版）
const products = ref([
  { id: 1, name: 'iPhone 14', category: '電子產品', price: 25000 },
  { id: 2, name: 'MacBook Pro', category: '電子產品', price: 55000 },
  { id: 3, name: '運動T恤', category: '服裝', price: 299 },
  { id: 4, name: '牛仔褲', category: '服裝', price: 1200 },
  { id: 5, name: '辦公椅', category: '家具', price: 3500 },
  { id: 6, name: '書桌', category: '家具', price: 8000 },
  { id: 7, name: 'Vue.js 教程', category: '書籍', price: 450 },
  { id: 8, name: 'JavaScript 指南', category: '書籍', price: 380 }
])

// 篩選條件
const searchKeyword = ref('')
const selectedCategory = ref('')

// 🚀 任務1：請完成關鍵字搜尋的計算屬性
const searchedProducts = computed(() => {
  // 在這裡實作關鍵字搜尋邏輯
  // 提示：當 searchKeyword 為空時，回傳所有商品
  // 當有關鍵字時，篩選出名稱包含關鍵字的商品（不區分大小寫）

  // 暫時回傳所有商品，學員需要實作篩選邏輯
  return products.value // 請修改這行
})

// 🚀 任務2：請完成分類篩選的計算屬性
const filteredProducts = computed(() => {
  // 在這裡實作分類篩選邏輯
  // 提示：先使用 searchedProducts 的結果，再根據 selectedCategory 篩選

  // 暫時回傳搜尋結果，學員需要加入分類篩選邏輯
  return searchedProducts.value // 請修改這行
})

// 🚀 任務3：請完成統計相關的計算屬性
const productCount = computed(() => {
  // 回傳篩選後的商品數量
  // 暫時回傳篩選結果的長度
  return filteredProducts.value.length // 請修改這行
})

const averagePrice = computed(() => {
  // 計算篩選後商品的平均價格（取整數）
  // 提示：當商品數量為0時，回傳0

  // 暫時回傳0，學員需要實作平均價格計算
  return 0 // 請修改這行
})
</script>

<style scoped>
.self-challenge {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}



.description {
  background: #f3e5f5;
  padding: 1rem;
  border-radius: 6px;
  margin: 1rem 0;
  border-left: 4px solid #9c27b0;
}

/* 練習任務區塊 */
.practice-tasks {
  background: #fff3e0;
  padding: 2rem;
  border-radius: 12px;
  margin: 2rem 0;
  border: 2px solid #ff9800;
}

.task-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1.5rem;
  margin-top: 1.5rem;
}

.task-card {
  background: white;
  border-radius: 8px;
  overflow: hidden;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  border: 1px solid #e0e0e0;
}

.task-header {
  background: #ff9800;
  color: white;
  padding: 1rem;
  display: flex;
  align-items: center;
  gap: 0.8rem;
}

.task-number {
  background: rgba(255, 255, 255, 0.2);
  width: 30px;
  height: 30px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  font-size: 1.1rem;
}

.task-header h4 {
  margin: 0;
  font-size: 1.1rem;
}

.task-content {
  padding: 1.5rem;
}

.task-content p {
  margin: 0.5rem 0;
}

.task-content strong {
  color: #d84315;
}

.task-content ul {
  margin: 0.5rem 0;
  padding-left: 1.2rem;
}

.task-content li {
  margin: 0.3rem 0;
  line-height: 1.4;
}

/* 其他區塊樣式 */
.demo-section {
  margin: 2rem 0;
  padding: 1.5rem;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  background: #fafafa;
}

.demo-section h3 {
  margin-top: 0;
  color: #333;
}

.filters {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1.5rem;
  margin: 1rem 0;
}

.filter-group {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.filter-group label {
  font-weight: bold;
  color: #333;
  font-size: 0.95rem;
}

.form-input,
.form-select {
  padding: 0.8rem;
  border: 2px solid #ddd;
  border-radius: 6px;
  font-size: 1rem;
  transition: border-color 0.3s;
}

.form-input:focus,
.form-select:focus {
  outline: none;
  border-color: #2196f3;
}

.stats-row {
  display: flex;
  gap: 2rem;
  flex-wrap: wrap;
}

.stat-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.8rem 1.2rem;
  background: white;
  border-radius: 6px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.stat-label {
  color: #666;
  font-weight: 500;
}

.stat-value {
  font-weight: bold;
  color: #1976d2;
  font-size: 1.1rem;
}

.product-list {
  min-height: 100px;
  background: white;
  border-radius: 6px;
  padding: 1rem;
}

.placeholder {
  text-align: center;
  color: #999;
  font-style: italic;
  padding: 2rem;
  background: #f9f9f9;
  border-radius: 6px;
  border: 2px dashed #ddd;
}

.no-products {
  text-align: center;
  color: #666;
  padding: 2rem;
  background: #f5f5f5;
  border-radius: 6px;
  margin: 1rem 0;
}

.product-item {
  background: white;
  border: 1px solid #e0e0e0;
  border-radius: 6px;
  padding: 1rem;
  margin: 0.5rem 0;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.product-item h4 {
  margin: 0 0 0.5rem 0;
  color: #333;
}

.product-item .category {
  background: #e3f2fd;
  color: #1976d2;
  padding: 0.2rem 0.5rem;
  border-radius: 12px;
  font-size: 0.8rem;
  margin-right: 0.5rem;
}

.product-item .price {
  font-size: 1.2rem;
  font-weight: bold;
  color: #d32f2f;
  margin: 0.5rem 0 0 0;
}

/* 提示區塊 */
.hint-section {
  background: #e8f5e8;
  padding: 1.5rem;
  border-radius: 8px;
  margin: 2rem 0;
}

.hint-section h4 {
  margin-top: 0;
  color: #2e7d32;
}

details {
  margin: 1rem 0;
  border: 1px solid #c8e6c9;
  border-radius: 4px;
}

summary {
  cursor: pointer;
  font-weight: bold;
  padding: 1rem;
  background: #c8e6c9;
  border-radius: 4px;
  transition: background-color 0.3s;
}

summary:hover {
  background: #a5d6a7;
}

pre {
  background: #2d3748;
  color: #e2e8f0;
  padding: 1rem;
  border-radius: 4px;
  overflow-x: auto;
  margin: 1rem 0;
  font-size: 0.9rem;
}

code {
  font-family: 'Fira Code', 'Courier New', monospace;
}

/* 響應式設計 */
@media (max-width: 768px) {
  .self-challenge {
    padding: 1rem;
  }

  .task-grid {
    grid-template-columns: 1fr;
  }

  .filters {
    grid-template-columns: 1fr;
  }

  .stats-row {
    flex-direction: column;
  }
}
</style>
