<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - Computed 計算屬性</h2>
    <p class="route-info">📍 路徑：/ComputedSamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>挑戰任務：</strong>建立商品篩選系統，實作各種計算屬性功能
    </p>

    <div class="challenge-section">
      <h3>🎯 挑戰清單</h3>
      <div class="task-list">
        <div class="task-item">
          <input type="checkbox" id="task1">
          <label for="task1">1. 篩選條件設定 - 搜尋、分類、價格範圍</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task2">
          <label for="task2">2. 統計資訊計算 - 商品數量與價格統計</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task3">
          <label for="task3">3. 商品列表渲染 - 動態篩選結果顯示</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task4">
          <label for="task4">4. 多層計算屬性 - 鏈式資料處理</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task5">
          <label for="task5">5. 重置篩選功能 - 表單狀態管理</label>
        </div>
      </div>
    </div>

    <div class="implementation-section">
      <h3>👨‍💻 實作練習詳情</h3>
      <p class="implementation-intro">
        📋 <strong>請完成商品篩選系統的各項計算屬性：</strong>
      </p>

      <div class="implementation-list">
        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">1.</span>
            <span class="function-name">搜尋功能計算屬性</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            實作 searchedProducts 計算屬性，根據關鍵字篩選商品名稱
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>搜尋範圍：</strong>商品名稱（name 欄位）</li>
                <li><strong>搜尋方式：</strong>不區分大小寫的關鍵字匹配</li>
                <li><strong>空關鍵字：</strong>回傳所有商品</li>
                <li><strong>即時搜尋：</strong>輸入變化時自動更新結果</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>使用 computed 定義 searchedProducts</li>
                <li>使用 filter 方法篩選商品陣列</li>
                <li>使用 toLowerCase() 和 includes() 進行不區分大小寫搜尋</li>
                <li>處理 searchKeyword 為空的情況</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">2.</span>
            <span class="function-name">分類篩選計算屬性</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            實作 filteredProducts 計算屬性，在搜尋結果基礎上進行分類篩選
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>資料來源：</strong>基於 searchedProducts 的結果</li>
                <li><strong>篩選條件：</strong>根據 selectedCategory 篩選商品類別</li>
                <li><strong>全部分類：</strong>selectedCategory 為空時顯示所有結果</li>
                <li><strong>鏈式處理：</strong>在搜尋結果基礎上進一步篩選</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>依賴 searchedProducts 計算屬性</li>
                <li>根據 selectedCategory 進行二次篩選</li>
                <li>處理空分類選項的情況</li>
                <li>確保計算屬性的依賴關係正確</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">3.</span>
            <span class="function-name">價格篩選計算屬性</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            實作 priceFilteredProducts 計算屬性，在分類篩選基礎上進行價格範圍篩選
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>資料來源：</strong>基於 filteredProducts 的結果</li>
                <li><strong>價格範圍：</strong>根據 minPrice 和 maxPrice 篩選</li>
                <li><strong>範圍包含：</strong>商品價格 >= minPrice 且 <= maxPrice</li>
                <li><strong>邊界處理：</strong>處理無效價格範圍的情況</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>依賴 filteredProducts 計算屬性</li>
                <li>使用數值比較進行價格範圍篩選</li>
                <li>處理 minPrice 和 maxPrice 的邊界值</li>
                <li>確保價格篩選邏輯的正確性</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">4.</span>
            <span class="function-name">排序計算屬性</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            實作 finalProducts 計算屬性，在價格篩選基礎上進行排序處理
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>資料來源：</strong>基於 priceFilteredProducts 的結果</li>
                <li><strong>排序選項：</strong>name-asc, name-desc, price-asc, price-desc</li>
                <li><strong>名稱排序：</strong>使用 localeCompare 進行本地化排序</li>
                <li><strong>價格排序：</strong>使用數值比較進行排序</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>依賴 priceFilteredProducts 計算屬性</li>
                <li>根據 sortBy 值執行不同排序邏輯</li>
                <li>實作字串和數值的雙向排序</li>
                <li>處理無排序選項時的預設狀態</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">5.</span>
            <span class="function-name">統計資訊計算屬性</span>
            <span class="difficulty hard">困難</span>
          </div>
          <div class="function-description">
            實作 productStats 計算屬性，提供最終結果的統計資訊
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>資料來源：</strong>基於 finalProducts 的結果</li>
                <li><strong>統計項目：</strong>count, averagePrice, maxPrice, minPrice</li>
                <li><strong>數值處理：</strong>平均價格保留到整數，避免小數點</li>
                <li><strong>空陣列處理：</strong>當沒有商品時所有統計值為 0</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>依賴 finalProducts 計算屬性</li>
                <li>計算商品數量和價格統計</li>
                <li>使用 Math.max, Math.min, reduce 進行統計</li>
                <li>處理空陣列的邊界情況</li>
              </ul>
            </div>
          </div>
        </div>
      </div>

      <div class="development-flow">
        <h4>📋 開發流程建議</h4>
        <div class="flow-steps">
          <div class="flow-step">
            <div class="step-number">1</div>
            <div class="step-content">
              <strong>搜尋功能</strong>
              <p>先實作基本的關鍵字搜尋計算屬性</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">2</div>
            <div class="step-content">
              <strong>分類篩選</strong>
              <p>在搜尋基礎上加入分類篩選</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">3</div>
            <div class="step-content">
              <strong>價格篩選</strong>
              <p>加入價格範圍的篩選功能</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">4</div>
            <div class="step-content">
              <strong>排序與統計</strong>
              <p>最後加入排序和統計功能</p>
            </div>
          </div>
        </div>
      </div>

      <div class="hint-section">
        <h4>💡 開發提示</h4>
        <details>
          <summary>點擊查看開發提示</summary>
          <div class="hints">
            <h5>計算屬性設計原則：</h5>
            <ul>
              <li><strong>依賴鏈：</strong>合理設計計算屬性的依賴關係</li>
              <li><strong>緩存效果：</strong>相同依賴值時會使用緩存結果</li>
              <li><strong>純函數：</strong>避免在計算屬性中產生副作用</li>
              <li><strong>性能考量：</strong>複雜計算可考慮拆分為多個計算屬性</li>
            </ul>

            <h5>常見問題解決：</h5>
            <ul>
              <li><strong>計算不更新：</strong>檢查依賴的響應式變數是否正確</li>
              <li><strong>效能問題：</strong>避免在計算屬性中做重複的複雜運算</li>
              <li><strong>排序混亂：</strong>確保排序函數回傳正確的比較值</li>
              <li><strong>統計錯誤：</strong>處理空陣列和無效數值的情況</li>
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
/* 自我試煉樣式 */
.self-challenge {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
  font-family: 'Arial', sans-serif;
}

.route-info {
  background: #e3f2fd;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  font-family: monospace;
  font-size: 0.9rem;
  color: #1976d2;
  margin-bottom: 1rem;
}

.description {
  font-size: 1.1rem;
  color: #495057;
  margin-bottom: 2rem;
  line-height: 1.6;
}

.challenge-section {
  background: #f8f9fa;
  padding: 2rem;
  border-radius: 12px;
  margin-bottom: 2rem;
  border-left: 5px solid #28a745;
}

.challenge-section h3 {
  color: #28a745;
  margin-bottom: 1.5rem;
  font-size: 1.5rem;
}

.task-list {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.task-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1rem;
  background: white;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s ease;
}

.task-item:hover {
  transform: translateX(10px);
}

.task-item input[type="checkbox"] {
  width: 20px;
  height: 20px;
  accent-color: #28a745;
}

.task-item label {
  font-size: 1.1rem;
  color: #495057;
  cursor: pointer;
  flex: 1;
}

.implementation-section {
  background: white;
  padding: 2rem;
  border-radius: 12px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.implementation-section h3 {
  color: #495057;
  margin-bottom: 1rem;
  font-size: 1.8rem;
}

.implementation-intro {
  font-size: 1.1rem;
  color: #6c757d;
  margin-bottom: 2rem;
  line-height: 1.6;
}

.implementation-list {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.implementation-item {
  border: 1px solid #e9ecef;
  border-radius: 12px;
  overflow: hidden;
  transition: box-shadow 0.3s ease;
}

.implementation-item:hover {
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.15);
}

.function-header {
  background: linear-gradient(135deg, #28a745 0%, #20c997 100%);
  color: white;
  padding: 1.5rem;
  display: flex;
  align-items: center;
  gap: 1rem;
}

.function-number {
  background: rgba(255, 255, 255, 0.2);
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  font-size: 1.2rem;
}

.function-name {
  flex: 1;
  font-size: 1.3rem;
  font-weight: 600;
}

.difficulty {
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.9rem;
  font-weight: bold;
  text-transform: uppercase;
}

.difficulty.easy {
  background: #d4edda;
  color: #155724;
}

.difficulty.medium {
  background: #fff3cd;
  color: #856404;
}

.difficulty.hard {
  background: #f8d7da;
  color: #721c24;
}

.function-description {
  padding: 2rem;
}

.spec-details {
  background: #f8f9fa;
  padding: 1.5rem;
  border-radius: 8px;
  margin: 1.5rem 0;
  border-left: 4px solid #17a2b8;
}

.spec-details strong {
  color: #17a2b8;
}

.spec-details ul {
  margin: 1rem 0 0 0;
  padding-left: 1.5rem;
}

.spec-details li {
  margin-bottom: 0.5rem;
  line-height: 1.5;
}

.task-requirements {
  background: #fff3cd;
  padding: 1.5rem;
  border-radius: 8px;
  border-left: 4px solid #ffc107;
}

.task-requirements h5 {
  color: #856404;
  margin: 0 0 1rem 0;
  font-size: 1.1rem;
}

.task-requirements ul {
  margin: 0;
  padding-left: 1.5rem;
}

.task-requirements li {
  margin-bottom: 0.5rem;
  color: #856404;
  line-height: 1.5;
}

.development-flow {
  background: #e8f5e8;
  padding: 2rem;
  border-radius: 12px;
  margin: 2rem 0;
}

.development-flow h4 {
  color: #28a745;
  margin-bottom: 1.5rem;
  font-size: 1.3rem;
}

.flow-steps {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1.5rem;
}

.flow-step {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  display: flex;
  align-items: flex-start;
  gap: 1rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.step-number {
  background: #28a745;
  color: white;
  width: 30px;
  height: 30px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  flex-shrink: 0;
}

.step-content strong {
  color: #28a745;
  display: block;
  margin-bottom: 0.5rem;
}

.step-content p {
  margin: 0;
  color: #6c757d;
  font-size: 0.9rem;
  line-height: 1.4;
}

.hint-section {
  background: #fff3cd;
  padding: 2rem;
  border-radius: 12px;
  margin-top: 2rem;
  border-left: 4px solid #ffc107;
}

.hint-section h4 {
  color: #856404;
  margin-bottom: 1rem;
  font-size: 1.3rem;
}

.hint-section details summary {
  cursor: pointer;
  font-weight: bold;
  color: #856404;
  margin-bottom: 1rem;
}

.hints h5 {
  color: #856404;
  margin: 1.5rem 0 1rem 0;
  font-size: 1.1rem;
}

.hints ul {
  margin: 0 0 1rem 0;
  padding-left: 1.5rem;
}

.hints li {
  margin-bottom: 0.5rem;
  color: #856404;
  line-height: 1.5;
}

.hints strong {
  color: #d39e00;
}

@media (max-width: 768px) {
  .self-challenge {
    padding: 1rem;
  }

  .function-header {
    flex-direction: column;
    text-align: center;
    gap: 1rem;
  }

  .flow-steps {
    grid-template-columns: 1fr;
  }

  .task-item {
    transform: none;
  }

  .task-item:hover {
    transform: none;
  }
}
</style>
