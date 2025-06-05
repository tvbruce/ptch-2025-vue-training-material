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
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作關鍵字搜尋的計算屬性</li>
                <li>處理空搜尋條件的情況</li>
                <li>實現不區分大小寫的搜尋</li>
                <li>使用 filter() 和 includes() 方法</li>
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
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>結合關鍵字搜尋結果進行分類篩選</li>
                <li>處理空分類選擇的情況</li>
                <li>實現計算屬性的鏈式依賴</li>
                <li>確保篩選邏輯的正確性</li>
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
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作價格範圍篩選功能</li>
                <li>處理價格邊界條件</li>
                <li>確保篩選邏輯的準確性</li>
                <li>優化計算屬性的性能</li>
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
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>計算篩選後商品的統計資訊</li>
                <li>處理空陣列的邊界情況</li>
                <li>使用 reduce 方法計算總價</li>
                <li>格式化數值顯示</li>
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
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作多種排序方式</li>
                <li>處理字串和數值的不同排序邏輯</li>
                <li>確保排序的穩定性</li>
                <li>優化排序算法的性能</li>
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
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>重置所有篩選條件到初始狀態</li>
                <li>確保所有響應式變數正確重置</li>
                <li>提供良好的用戶體驗</li>
                <li>測試重置功能的完整性</li>
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


  </div>
</template>

<script setup>
// 此文件僅包含自我試煉的題目說明和實作指引
// 實際的程式碼實作請在 SelfChallengeAnsweringArea.vue 中完成
</script>

<style scoped>
/* 使用統一的自我試煉樣式 */
@import '@/assets/main.css';
</style>
