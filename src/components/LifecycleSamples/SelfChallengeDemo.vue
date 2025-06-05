<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - Lifecycle 生命週期</h2>
    <p class="route-info">📍 路徑：/LifecycleSamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>挑戰任務：</strong>建立一個整合計時器和資料載入的應用，實作各種生命週期鉤子
    </p>

    <div class="challenge-section">
      <h3>🎯 挑戰清單</h3>
      <div class="task-list">
        <div class="task-item">
          <input type="checkbox" id="task1">
          <label for="task1">1. 多功能計時器 - 開始、暫停、重置功能</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task2">
          <label for="task2">2. 資料載入管理 - 模擬 API 載入與進度顯示</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task3">
          <label for="task3">3. 生命週期追蹤 - 事件日誌記錄系統</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task4">
          <label for="task4">4. 組件掛載初始化 - onMounted 鉤子應用</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task5">
          <label for="task5">5. 組件銷毀清理 - onBeforeUnmount 資源釋放</label>
        </div>
      </div>
    </div>

    <div class="implementation-section">
      <h3>👨‍💻 實作練習詳情</h3>
      <p class="implementation-intro">
        📋 <strong>請完成計時器和資料載入應用的各項生命週期功能：</strong>
      </p>

      <div class="implementation-list">
        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">1.</span>
            <span class="function-name">多功能計時器</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            實作完整的計時器功能，包含開始、暫停、重置和統計記錄
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>計時器顯示：</strong>以 MM:SS 格式顯示運行時間</li>
                <li><strong>狀態管理：</strong>已停止、運行中、已暫停</li>
                <li><strong>統計記錄：</strong>總啟動次數、總暫停次數、最長運行時間</li>
                <li><strong>計時器控制：</strong>防止重複啟動，狀態同步</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作 startTimer 方法使用 setInterval</li>
                <li>實作 pauseTimer 方法清除計時器</li>
                <li>實作 resetTimer 方法重置所有狀態</li>
                <li>實作 formatTime 方法格式化時間顯示</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">2.</span>
            <span class="function-name">資料載入管理</span>
            <span class="difficulty hard">困難</span>
          </div>
          <div class="function-description">
            實作模擬 API 資料載入功能，包含進度顯示和錯誤處理
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>載入類型：</strong>用戶資料載入、新聞資料載入</li>
                <li><strong>進度顯示：</strong>載入進度條和百分比顯示</li>
                <li><strong>錯誤處理：</strong>載入失敗時的錯誤訊息和重試功能</li>
                <li><strong>狀態管理：</strong>載入中、成功、失敗狀態切換</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作 loadUserData 方法模擬用戶資料載入</li>
                <li>實作 loadNewsData 方法模擬新聞資料載入</li>
                <li>使用 setTimeout 模擬 API 載入時間</li>
                <li>實作進度更新和錯誤處理機制</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">3.</span>
            <span class="function-name">生命週期追蹤</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            建立生命週期事件的日誌記錄系統，追蹤組件狀態變化
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>日誌格式：</strong>時間戳、事件類型、詳細資訊</li>
                <li><strong>事件追蹤：</strong>組件掛載、資料變化、計時器狀態</li>
                <li><strong>日誌顯示：</strong>可滾動的日誌容器，最新事件在底部</li>
                <li><strong>日誌管理：</strong>清空日誌功能，避免記憶體累積</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作 addLifecycleLog 方法記錄事件</li>
                <li>使用 watch 監聽資料變化並記錄</li>
                <li>在關鍵操作時自動記錄日誌</li>
                <li>實作 clearLogs 方法清空日誌</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">4.</span>
            <span class="function-name">組件掛載初始化</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            使用 onMounted 生命週期鉤子進行組件初始化工作
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>初始化時機：</strong>組件掛載到 DOM 後執行</li>
                <li><strong>初始化任務：</strong>記錄掛載事件、初始化計時器狀態</li>
                <li><strong>資料預載：</strong>可選擇性載入初始資料</li>
                <li><strong>狀態設定：</strong>設定組件的初始狀態</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>在 onMounted 中記錄組件掛載事件</li>
                <li>初始化計時器相關狀態</li>
                <li>設定初始的生命週期日誌</li>
                <li>可選擇性執行初始資料載入</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">5.</span>
            <span class="function-name">組件銷毀清理</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            使用 onBeforeUnmount 生命週期鉤子進行資源清理工作
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>清理時機：</strong>組件銷毀前執行清理工作</li>
                <li><strong>計時器清理：</strong>清除所有活動的計時器</li>
                <li><strong>事件清理：</strong>移除事件監聽器避免記憶體洩漏</li>
                <li><strong>狀態記錄：</strong>記錄組件銷毀事件</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>在 onBeforeUnmount 中清除計時器</li>
                <li>記錄組件銷毀事件到日誌</li>
                <li>清理所有活動的 setInterval</li>
                <li>確保無記憶體洩漏問題</li>
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
              <strong>基礎設定</strong>
              <p>建立響應式資料和基本方法</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">2</div>
            <div class="step-content">
              <strong>計時器功能</strong>
              <p>實作計時器的核心功能</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">3</div>
            <div class="step-content">
              <strong>資料載入</strong>
              <p>加入模擬 API 載入功能</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">4</div>
            <div class="step-content">
              <strong>生命週期</strong>
              <p>加入生命週期鉤子和清理</p>
            </div>
          </div>
        </div>
      </div>

      <div class="hint-section">
        <h4>💡 開發提示</h4>
        <details>
          <summary>點擊查看開發提示</summary>
          <div class="hints">
            <h5>生命週期鉤子使用：</h5>
            <ul>
              <li><strong>onMounted：</strong>組件掛載後執行，適合初始化工作</li>
              <li><strong>onBeforeUnmount：</strong>組件銷毀前執行，適合清理工作</li>
              <li><strong>watch：</strong>監聽資料變化，可以記錄狀態變化</li>
              <li><strong>watchEffect：</strong>自動追蹤依賴，適合響應式更新</li>
            </ul>

            <h5>常見問題解決：</h5>
            <ul>
              <li><strong>計時器洩漏：</strong>必須在組件銷毀前清除 setInterval</li>
              <li><strong>狀態同步：</strong>確保計時器狀態與 UI 狀態一致</li>
              <li><strong>非同步處理：</strong>正確處理載入狀態和錯誤情況</li>
              <li><strong>記憶體管理：</strong>避免日誌無限累積導致記憶體問題</li>
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
  border-left: 5px solid #17a2b8;
}

.challenge-section h3 {
  color: #17a2b8;
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
  accent-color: #17a2b8;
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
  background: linear-gradient(135deg, #17a2b8 0%, #20c997 100%);
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
