<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - Watcher 觀察者</h2>
    <p class="route-info">📍 路徑：/WatcherSamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>挑戰任務：</strong>建立一個資料監控系統，實作各種 watch 監聽功能
    </p>

    <div class="challenge-section">
      <h3>🎯 挑戰清單</h3>
      <div class="task-list">
        <div class="task-item">
          <input type="checkbox" id="task1">
          <label for="task1">1. 基本資料監聽 - 監聽使用者輸入變化</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task2">
          <label for="task2">2. 深度對象監聽 - 監聽複雜對象內部變化</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task3">
          <label for="task3">3. 計算屬性監聽 - 監聽計算結果變化</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task4">
          <label for="task4">4. 異步操作監聽 - 搜尋與防抖處理</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task5">
          <label for="task5">5. watchEffect 應用 - 自動依賴追蹤</label>
        </div>
      </div>
    </div>

    <div class="implementation-section">
      <h3>👨‍💻 實作練習詳情</h3>
      <p class="implementation-intro">
        📋 <strong>請完成資料監控系統的各項 watch 監聽功能：</strong>
      </p>

      <div class="implementation-list">
        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">1.</span>
            <span class="function-name">基本資料監聽</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            使用 watch 監聽基本資料類型的變化，記錄變化日誌
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>監聽目標：</strong>用戶名稱、年齡、郵箱輸入</li>
                <li><strong>變化記錄：</strong>記錄舊值到新值的變化</li>
                <li><strong>時間戳記：</strong>每次變化都記錄時間</li>
                <li><strong>日誌格式：</strong>時間、欄位、舊值、新值</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>使用 watch 監聽 userName, userAge, userEmail</li>
                <li>實作 addWatchLog 方法記錄變化</li>
                <li>在監聽器中記錄新值和舊值</li>
                <li>實作 clearWatchLogs 方法清空日誌</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">2.</span>
            <span class="function-name">深度對象監聽</span>
            <span class="difficulty hard">困難</span>
          </div>
          <div class="function-description">
            使用深度監聽追蹤複雜對象內部屬性的變化
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>監聽對象：</strong>用戶資料對象（姓名、職業、地址、技能）</li>
                <li><strong>深度監聽：</strong>監聽巢狀對象和陣列的變化</li>
                <li><strong>變化統計：</strong>總變更次數、最後變更時間</li>
                <li><strong>熱點分析：</strong>統計最頻繁變更的欄位</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>使用 watch 深度監聽 userProfile 對象</li>
                <li>設定 { deep: true } 選項</li>
                <li>實作 addSkill 和 removeSkill 方法</li>
                <li>統計變化次數和最頻繁變更欄位</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">3.</span>
            <span class="function-name">計算屬性監聽</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            監聽計算屬性的變化，建立計算歷史記錄
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>計算器：</strong>兩個數字和運算符的計算</li>
                <li><strong>結果監聽：</strong>監聽計算結果的變化</li>
                <li><strong>歷史記錄：</strong>保存每次計算的完整記錄</li>
                <li><strong>表達式格式：</strong>數字1 運算符 數字2 = 結果</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作 calculationResult 計算屬性</li>
                <li>使用 watch 監聽計算結果變化</li>
                <li>記錄完整的計算表達式和結果</li>
                <li>實作 clearHistory 方法清空歷史</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">4.</span>
            <span class="function-name">異步操作監聽</span>
            <span class="difficulty hard">困難</span>
          </div>
          <div class="function-description">
            監聽搜尋關鍵字變化，實作防抖搜尋和統計分析
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>搜尋功能：</strong>根據關鍵字搜尋模擬資料</li>
                <li><strong>防抖處理：</strong>延遲執行搜尋避免頻繁調用</li>
                <li><strong>載入狀態：</strong>顯示搜尋中狀態和進度</li>
                <li><strong>搜尋統計：</strong>搜尋次數、響應時間、熱門關鍵字</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>使用 watch 監聽 searchKeyword 變化</li>
                <li>實作 performSearch 方法執行搜尋</li>
                <li>使用 setTimeout 實作防抖機制</li>
                <li>記錄搜尋統計和分析數據</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">5.</span>
            <span class="function-name">watchEffect 應用</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            使用 watchEffect 實作自動依賴追蹤和響應式更新
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>自動追蹤：</strong>自動追蹤計算器輸入的變化</li>
                <li><strong>即時響應：</strong>任一輸入變化時立即響應</li>
                <li><strong>副作用處理：</strong>更新相關的統計和日誌</li>
                <li><strong>清理機制：</strong>組件銷毀時清理副作用</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>使用 watchEffect 追蹤 num1, num2, operator</li>
                <li>實作自動計算和結果更新</li>
                <li>在副作用中更新相關統計</li>
                <li>理解 watchEffect 與 watch 的差異</li>
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
              <strong>基礎監聽</strong>
              <p>從簡單的 watch 開始，監聽基本資料</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">2</div>
            <div class="step-content">
              <strong>深度監聽</strong>
              <p>學習深度監聽複雜對象的變化</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">3</div>
            <div class="step-content">
              <strong>計算監聽</strong>
              <p>監聽計算屬性並記錄歷史</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">4</div>
            <div class="step-content">
              <strong>進階應用</strong>
              <p>異步監聽和 watchEffect 應用</p>
            </div>
          </div>
        </div>
      </div>

      <div class="hint-section">
        <h4>💡 開發提示</h4>
        <details>
          <summary>點擊查看開發提示</summary>
          <div class="hints">
            <h5>watch 使用技巧：</h5>
            <ul>
              <li><strong>基本語法：</strong>watch(source, callback, options)</li>
              <li><strong>深度監聽：</strong>{ deep: true } 監聽對象內部變化</li>
              <li><strong>立即執行：</strong>{ immediate: true } 立即執行一次</li>
              <li><strong>watchEffect：</strong>自動追蹤依賴，無需指定監聽目標</li>
            </ul>

            <h5>常見問題解決：</h5>
            <ul>
              <li><strong>性能問題：</strong>深度監聽大對象時要注意性能</li>
              <li><strong>防抖處理：</strong>高頻變化時使用 setTimeout 防抖</li>
              <li><strong>記憶體洩漏：</strong>記得在組件銷毀時停止監聽</li>
              <li><strong>循環依賴：</strong>避免在監聽器中修改被監聽的資料</li>
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
  border-left: 5px solid #6f42c1;
}

.challenge-section h3 {
  color: #6f42c1;
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
  accent-color: #6f42c1;
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
  background: linear-gradient(135deg, #6f42c1 0%, #9c27b0 100%);
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
