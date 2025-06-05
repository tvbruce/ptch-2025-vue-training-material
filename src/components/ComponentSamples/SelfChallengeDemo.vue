<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - 組件化開發</h2>
    <p class="route-info">📍 路徑：/ComponentSamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>挑戰任務：</strong>建立一個任務管理系統，練習組件化開發的核心概念
    </p>

    <div class="challenge-section">
      <h3>🎯 挑戰清單</h3>
      <div class="task-list">
        <div class="task-item">
          <input type="checkbox" id="task1">
          <label for="task1">1. 實作任務統計 - 計算屬性與數據展示</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task2">
          <label for="task2">2. 建立 TaskForm 組件 - 表單處理與事件發送</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task3">
          <label for="task3">3. 實作任務篩選 - 動態數據篩選與按鈕切換</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task4">
          <label for="task4">4. 建立 TaskItem 組件 - Props 傳遞與事件通信</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task5">
          <label for="task5">5. 建立 Card 組件 - 插槽使用與內容自定義</label>
        </div>
      </div>
    </div>

    <div class="implementation-section">
      <h3>👨‍💻 實作練習詳情</h3>
      <p class="implementation-intro">
        📋 <strong>請按照以下順序完成任務管理系統的組件化開發：</strong>
      </p>

      <div class="implementation-list">
        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">1.</span>
            <span class="function-name">任務統計功能</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            實作任務統計的計算屬性，顯示總任務、已完成、待完成和完成率
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>統計卡片：</strong>總任務數、已完成數、待完成數、完成率</li>
                <li><strong>計算屬性：</strong>totalTasks, completedCount, pendingCount, completionRate</li>
                <li><strong>數據來源：</strong>tasks 陣列中的 completed 屬性</li>
                <li><strong>完成率：</strong>百分比計算並四捨五入</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>使用 computed 實作所有統計計算</li>
                <li>處理空陣列的邊界情況</li>
                <li>確保數據響應式更新</li>
                <li>實現數據即時同步</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">2.</span>
            <span class="function-name">TaskForm 組件</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            建立新增任務的表單組件，處理表單資料與父子組件通信
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>表單欄位：</strong>任務標題、任務描述、優先級選擇</li>
                <li><strong>表單驗證：</strong>標題必填、長度限制</li>
                <li><strong>事件發送：</strong>add-task 事件傳遞表單資料</li>
                <li><strong>表單重置：</strong>提交後清空表單內容</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>建立 TaskForm.vue 組件檔案</li>
                <li>使用 v-model 綁定表單資料</li>
                <li>實作表單驗證邏輯</li>
                <li>使用 emit 發送 add-task 事件</li>
                <li>在父組件中引入並使用 TaskForm</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">3.</span>
            <span class="function-name">任務篩選功能</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            實作任務篩選機制，提供多種篩選條件的動態切換
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>篩選選項：</strong>全部、待完成、已完成、高優先級、中優先級、低優先級</li>
                <li><strong>篩選邏輯：</strong>根據任務的 completed 和 priority 屬性</li>
                <li><strong>視覺回饋：</strong>當前選中的篩選按鈕高亮顯示</li>
                <li><strong>數據更新：</strong>篩選條件改變時即時更新任務列表</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>定義篩選器資料結構 (filters 陣列)</li>
                <li>實作 currentFilter 狀態管理</li>
                <li>使用 v-for 動態渲染篩選按鈕</li>
                <li>實作 filteredTasks 計算屬性</li>
                <li>處理按鈕點擊事件與樣式切換</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">4.</span>
            <span class="function-name">TaskItem 組件</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            建立任務項目顯示組件，處理任務資料展示與互動操作
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>Props：</strong>task 物件（包含 id, title, description, priority, completed）</li>
                <li><strong>顯示內容：</strong>任務標題、描述、優先級標籤</li>
                <li><strong>互動功能：</strong>標記完成/取消完成、刪除任務</li>
                <li><strong>事件發送：</strong>toggle-complete, delete-task</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>建立 TaskItem.vue 組件檔案</li>
                <li>定義 props 接收任務資料</li>
                <li>實作優先級中文轉換（計算屬性）</li>
                <li>處理完成狀態的視覺樣式</li>
                <li>實作刪除確認機制</li>
                <li>在父組件中使用 v-for 渲染任務列表</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">5.</span>
            <span class="function-name">Card 組件</span>
            <span class="difficulty hard">困難</span>
          </div>
          <div class="function-description">
            建立可重用的卡片組件，實作插槽機制提供靈活的內容結構
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>Props：</strong>title（卡片標題）, color（主題色彩）</li>
                <li><strong>插槽類型：</strong>header 具名插槽、預設插槽、footer 具名插槽</li>
                <li><strong>樣式主題：</strong>支援多種顏色主題（primary, success, info 等）</li>
                <li><strong>響應式設計：</strong>適配不同螢幕尺寸</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>建立 Card.vue 組件檔案</li>
                <li>實作具名插槽（header, footer）</li>
                <li>實作預設插槽（主要內容區域）</li>
                <li>使用 $slots 進行條件渲染</li>
                <li>實作動態樣式切換（:class 綁定）</li>
                <li>創建多個卡片實例展示不同用法</li>
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
              <strong>資料準備</strong>
              <p>先實作統計計算屬性，確保資料邏輯正確</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">2</div>
            <div class="step-content">
              <strong>組件建立</strong>
              <p>依序建立 TaskForm、TaskItem、Card 組件檔案</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">3</div>
            <div class="step-content">
              <strong>組件整合</strong>
              <p>在父組件中引入並使用子組件</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">4</div>
            <div class="step-content">
              <strong>功能驗證</strong>
              <p>測試篩選功能和組件間的事件通信</p>
            </div>
          </div>
        </div>
      </div>

      <div class="hint-section">
        <h4>💡 開發提示</h4>
        <details>
          <summary>點擊查看開發提示</summary>
          <div class="hints">
            <h5>組件化開發要點：</h5>
            <ul>
              <li><strong>Props Down：</strong>父組件向子組件傳遞資料</li>
              <li><strong>Events Up：</strong>子組件向父組件發送事件</li>
              <li><strong>插槽使用：</strong>具名插槽與預設插槽的靈活應用</li>
              <li><strong>計算屬性：</strong>用於資料處理和狀態計算</li>
              <li><strong>組件檔案：</strong>放置在 components/ComponentSamples/components/SelfChallengeAnswering/ 目錄</li>
            </ul>

            <h5>常見問題解決：</h5>
            <ul>
              <li><strong>組件未顯示：</strong>檢查是否正確 import 和註冊組件</li>
              <li><strong>事件未觸發：</strong>確認 emit 事件名稱與父組件監聽的事件名稱一致</li>
              <li><strong>插槽未生效：</strong>檢查 slot name 是否正確，是否使用 template 標籤</li>
              <li><strong>樣式未套用：</strong>確認 :class 綁定和 CSS 類別名稱是否正確</li>
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
  border-left: 5px solid #20c997;
}

.challenge-section h3 {
  color: #20c997;
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
  accent-color: #20c997;
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
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
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
