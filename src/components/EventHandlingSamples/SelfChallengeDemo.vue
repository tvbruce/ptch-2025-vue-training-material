<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - Event 事件處理</h2>
    <p class="route-info">📍 路徑：/EventHandlingSamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>挑戰任務：</strong>建立一個互動遊戲應用，實作各種事件處理功能
    </p>

    <div class="challenge-section">
      <h3>🎯 挑戰清單</h3>
      <div class="task-list">
        <div class="task-item">
          <input type="checkbox" id="task1">
          <label for="task1">1. 點擊計數器 - 處理點擊與雙擊事件</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task2">
          <label for="task2">2. 鍵盤操作 - WASD 移動控制與按鍵狀態</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task3">
          <label for="task3">3. 滑鼠追蹤 - 滑鼠移動與軌跡效果</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task4">
          <label for="task4">4. 表單事件 - 輸入、焦點與特殊按鍵</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task5">
          <label for="task5">5. 事件日誌 - 記錄與追蹤使用者操作</label>
        </div>
      </div>
    </div>

    <div class="implementation-section">
      <h3>👨‍💻 實作練習詳情</h3>
      <p class="implementation-intro">
        📋 <strong>請完成互動遊戲應用的各項事件處理功能：</strong>
      </p>

      <div class="implementation-list">
        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">1.</span>
            <span class="function-name">點擊計數器系統</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            實作點擊計數器，包含連擊系統和統計記錄
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>點擊計數：</strong>記錄總點擊次數</li>
                <li><strong>連擊系統：</strong>連續點擊累計連擊數，3秒內無點擊則重置</li>
                <li><strong>雙擊處理：</strong>雙擊獲得額外分數或特殊效果</li>
                <li><strong>統計記錄：</strong>最高連擊數記錄</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作 handleClick 方法處理點擊事件</li>
                <li>實作 handleDoubleClick 方法處理雙擊事件</li>
                <li>使用 setInterval 管理連擊計時器</li>
                <li>實作 resetCounter 方法重置所有計數</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">2.</span>
            <span class="function-name">鍵盤遊戲控制</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            實作鍵盤控制的簡單遊戲，包含角色移動和按鍵狀態追蹤
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>移動控制：</strong>WASD 或方向鍵控制角色移動</li>
                <li><strong>按鍵狀態：</strong>顯示當前按下的按鍵</li>
                <li><strong>遊戲元素：</strong>隨機生成金幣和炸彈</li>
                <li><strong>分數系統：</strong>收集金幣增加分數，撞到炸彈減少生命</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作 handleKeyDown 方法處理按鍵按下</li>
                <li>實作 handleKeyUp 方法處理按鍵釋放</li>
                <li>使用 Set 追蹤當前按下的按鍵</li>
                <li>實作角色移動和碰撞檢測邏輯</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">3.</span>
            <span class="function-name">滑鼠追蹤與軌跡</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            實作滑鼠追蹤功能，包含位置記錄和視覺軌跡效果
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>位置追蹤：</strong>即時顯示滑鼠座標</li>
                <li><strong>軌跡效果：</strong>滑鼠移動留下星星軌跡</li>
                <li><strong>區域檢測：</strong>偵測滑鼠進入/離開指定區域</li>
                <li><strong>右鍵事件：</strong>右鍵點擊計數和特殊處理</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作 handleMouseMove 方法追蹤滑鼠位置</li>
                <li>實作 handleMouseEnter/Leave 方法處理區域事件</li>
                <li>實作 handleRightClick 方法處理右鍵點擊</li>
                <li>管理滑鼠軌跡陣列和淡出效果</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">4.</span>
            <span class="function-name">表單事件處理</span>
            <span class="difficulty hard">困難</span>
          </div>
          <div class="function-description">
            實作完整的表單事件處理，包含即時搜尋和特殊按鍵處理
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>即時搜尋：</strong>輸入時自動搜尋並顯示結果</li>
                <li><strong>焦點事件：</strong>輸入框獲得/失去焦點的處理</li>
                <li><strong>特殊按鍵：</strong>Enter 確認搜尋，Escape 清空輸入</li>
                <li><strong>搜尋結果：</strong>根據關鍵字篩選顯示匹配項目</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作 handleInput 方法處理輸入事件</li>
                <li>實作 handleFocus/Blur 方法處理焦點事件</li>
                <li>實作 handleEnterKey/EscapeKey 方法處理特殊按鍵</li>
                <li>實作即時搜尋和結果篩選邏輯</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">5.</span>
            <span class="function-name">事件日誌系統</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            建立事件日誌記錄系統，追蹤和顯示所有使用者操作
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>事件記錄：</strong>記錄所有重要的使用者操作</li>
                <li><strong>時間戳記：</strong>每個事件都有準確的時間記錄</li>
                <li><strong>事件分類：</strong>按不同類型分類顯示事件</li>
                <li><strong>日誌管理：</strong>清空日誌和日誌數量限制</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作 addEventLog 方法記錄事件</li>
                <li>在各個事件處理方法中加入日誌記錄</li>
                <li>實作 clearEventLogs 方法清空日誌</li>
                <li>格式化顯示時間和事件資訊</li>
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
              <strong>基礎事件</strong>
              <p>先實作點擊和基本事件處理</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">2</div>
            <div class="step-content">
              <strong>鍵盤控制</strong>
              <p>加入鍵盤事件和遊戲邏輯</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">3</div>
            <div class="step-content">
              <strong>滑鼠追蹤</strong>
              <p>實作滑鼠事件和視覺效果</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">4</div>
            <div class="step-content">
              <strong>進階功能</strong>
              <p>完成表單事件和日誌系統</p>
            </div>
          </div>
        </div>
      </div>

      <div class="hint-section">
        <h4>💡 開發提示</h4>
        <details>
          <summary>點擊查看開發提示</summary>
          <div class="hints">
            <h5>事件處理技巧：</h5>
            <ul>
              <li><strong>事件物件：</strong>event.preventDefault() 阻止預設行為</li>
              <li><strong>事件修飾符：</strong>.prevent, .stop, .once, .passive</li>
              <li><strong>按鍵修飾符：</strong>.enter, .esc, .space, .up, .down</li>
              <li><strong>滑鼠事件：</strong>event.clientX/Y 獲取滑鼠座標</li>
            </ul>

            <h5>常見問題解決：</h5>
            <ul>
              <li><strong>事件重複：</strong>使用事件修飾符避免重複觸發</li>
              <li><strong>記憶體洩漏：</strong>組件銷毀時清除事件監聽器</li>
              <li><strong>效能問題：</strong>高頻事件（如 mousemove）要注意效能</li>
              <li><strong>鍵盤焦點：</strong>確保鍵盤事件的元素有正確焦點</li>
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
  border-left: 5px solid #e83e8c;
}

.challenge-section h3 {
  color: #e83e8c;
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
  accent-color: #e83e8c;
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
  background: linear-gradient(135deg, #e83e8c 0%, #ff6b9d 100%);
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
