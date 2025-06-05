<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - Computed 計算屬性</h2>
    <p class="route-info">📍 路徑：/ComputedSamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>學習目標：</strong>透過建立簡單的商品篩選功能，掌握 computed 計算屬性的基本用法
    </p>

    <div class="challenge-section">
      <h3>🎯 挑戰清單</h3>
      <div class="task-list">
        <div class="task-item">
          <input type="checkbox" id="task1">
          <label for="task1">1. 實作關鍵字搜尋功能（searchedProducts）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task2">
          <label for="task2">2. 實作分類篩選功能（filteredProducts）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task3">
          <label for="task3">3. 實作價格範圍篩選（priceFilteredProducts）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task4">
          <label for="task4">4. 計算統計資訊（總數、平均價格）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task5">
          <label for="task5">5. 實作排序功能</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task6">
          <label for="task6">6. 建立完整的商品篩選系統</label>
        </div>
      </div>
    </div>

    <div class="implementation-section">
      <h3>👨‍💻 實作練習詳情</h3>
      <p class="implementation-intro">
        📋 <strong>請在 &lt;script setup&gt; 區域完成以下計算屬性的實作：</strong>
      </p>

      <div class="implementation-list">
        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">1.</span>
            <span class="function-name">searchedProducts (computed)</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            根據關鍵字搜尋商品
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>搜尋邏輯：</strong>當 searchKeyword.value 有值時進行篩選</li>
                <li><strong>搜尋範圍：</strong>商品名稱（name 屬性）</li>
                <li><strong>不區分大小寫：</strong>使用 toLowerCase() 轉換</li>
                <li><strong>空值處理：</strong>searchKeyword 為空時返回所有商品</li>
                <li><strong>方法：</strong>使用 filter() 和 includes() 方法</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">2.</span>
            <span class="function-name">filteredProducts (computed)</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            結合搜尋和分類篩選
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>基礎資料：</strong>使用 searchedProducts.value 作為基礎</li>
                <li><strong>分類篩選：</strong>根據 selectedCategory.value 進行篩選</li>
                <li><strong>空值處理：</strong>selectedCategory 為空時顯示所有搜尋結果</li>
                <li><strong>篩選條件：</strong>商品的 category 屬性等於選擇的分類</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">3.</span>
            <span class="function-name">priceFilteredProducts (computed)</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            根據價格範圍篩選商品
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>基礎資料：</strong>使用 filteredProducts.value 作為基礎</li>
                <li><strong>價格範圍：</strong>minPrice.value 到 maxPrice.value</li>
                <li><strong>篩選條件：</strong>商品價格在指定範圍內</li>
                <li><strong>邊界處理：</strong>包含最小值和最大值</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">4.</span>
            <span class="function-name">productStats (computed)</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            計算商品統計資訊
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>總數：</strong>priceFilteredProducts.value.length</li>
                <li><strong>平均價格：</strong>使用 reduce 計算總價再除以數量</li>
                <li><strong>最高價格：</strong>使用 Math.max 找出最高價</li>
                <li><strong>最低價格：</strong>使用 Math.min 找出最低價</li>
                <li><strong>格式化：</strong>價格保留兩位小數</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">5.</span>
            <span class="function-name">sortedProducts (computed)</span>
            <span class="difficulty hard">困難</span>
          </div>
          <div class="function-description">
            根據選擇的排序方式排序商品
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>基礎資料：</strong>使用 priceFilteredProducts.value</li>
                <li><strong>排序選項：</strong>
                  <ul>
                    <li>'name-asc': 名稱升序</li>
                    <li>'name-desc': 名稱降序</li>
                    <li>'price-asc': 價格升序</li>
                    <li>'price-desc': 價格降序</li>
                  </ul>
                </li>
                <li><strong>預設：</strong>sortBy.value 為空時保持原順序</li>
                <li><strong>方法：</strong>使用 sort() 方法和比較函數</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">6.</span>
            <span class="function-name">resetFilters()</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            重置所有篩選條件
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>搜尋關鍵字：</strong>searchKeyword.value = ''</li>
                <li><strong>分類選擇：</strong>selectedCategory.value = ''</li>
                <li><strong>價格範圍：</strong>minPrice.value = 0, maxPrice.value = 1000</li>
                <li><strong>排序方式：</strong>sortBy.value = ''</li>
              </ul>
            </div>
          </div>
        </div>
      </div>

      <div class="hint-section">
        <h4>💡 開發提示</h4>
        <details>
          <summary>點擊查看開發提示</summary>
          <div class="hints">
            <h5>常用語法參考：</h5>
            <pre><code>// 計算屬性基本語法
const filteredList = computed(() => {
  return list.value.filter(item => condition)
})

// 陣列篩選方法
array.filter(item => item.name.includes(keyword))
array.filter(item => item.category === selectedCategory)

// 字串比較（不區分大小寫）
item.name.toLowerCase().includes(keyword.toLowerCase())

// 數值計算
const total = array.reduce((sum, item) => sum + item.price, 0)
const average = total / array.length

// 陣列排序
array.sort((a, b) => a.price - b.price) // 升序
array.sort((a, b) => b.price - a.price) // 降序</code></pre>

            <h5>重要概念：</h5>
            <ul>
              <li><strong>計算屬性：</strong>使用 computed() 包裝函數，會自動追蹤依賴</li>
              <li><strong>陣列方法：</strong>filter(), map(), reduce(), sort() 是常用的陣列處理方法</li>
              <li><strong>字串處理：</strong>toLowerCase() 和 includes() 用於不區分大小寫搜尋</li>
              <li><strong>數值計算：</strong>注意處理空陣列的情況，避免除以零</li>
              <li><strong>鏈式呼叫：</strong>可以將多個計算屬性串聯使用</li>
            </ul>
          </div>
        </details>
      </div>
    </div>

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
/* 使用統一的自我試煉樣式 */
@import '@/assets/self-challenge.css';
/* 樣式已在 src/assets/computed-properties.css 中定義 */
</style>
