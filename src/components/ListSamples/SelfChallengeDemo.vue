<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - v-for 列表渲染</h2>
    <p class="route-info">📍 路徑：/ListSamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>挑戰任務：</strong>建立學生成績管理系統，實作 v-for 列表渲染的各種功能
    </p>

    <div class="challenge-section">
      <h3>🎯 挑戰清單</h3>
      <div class="task-list">
        <div class="task-item">
          <input type="checkbox" id="task1">
          <label for="task1">1. 學生列表渲染 - 使用 v-for 顯示學生資料</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task2">
          <label for="task2">2. 新增學生功能 - 表單處理與資料新增</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task3">
          <label for="task3">3. 統計資料計算 - 計算屬性統計學生成績</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task4">
          <label for="task4">4. 編輯學生資料 - 資料修改與狀態管理</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task5">
          <label for="task5">5. 篩選與排序 - 動態資料篩選功能</label>
        </div>
      </div>
    </div>

    <div class="implementation-section">
      <h3>👨‍💻 實作練習詳情</h3>
      <p class="implementation-intro">
        📋 <strong>請完成學生成績管理系統的各項功能：</strong>
      </p>

      <div class="implementation-list">
        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">1.</span>
            <span class="function-name">學生列表渲染</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            使用 v-for 渲染學生列表，包含排序和篩選控制功能
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>資料結構：</strong>學生 ID、姓名、科目、分數</li>
                <li><strong>顯示方式：</strong>卡片式佈局，響應式網格</li>
                <li><strong>操作按鈕：</strong>按分數排序、顯示及格學生</li>
                <li><strong>互動功能：</strong>刪除學生、編輯學生</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>使用 v-for 遍歷 filteredStudents 陣列</li>
                <li>為每個項目設定唯一的 :key 屬性</li>
                <li>實作 sortByScore 排序功能</li>
                <li>實作篩選及格學生的切換功能</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">2.</span>
            <span class="function-name">新增學生功能</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            建立新增學生的表單介面，處理表單驗證與資料新增
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>表單欄位：</strong>學生姓名、科目、分數</li>
                <li><strong>資料驗證：</strong>必填欄位檢查、分數範圍驗證</li>
                <li><strong>ID 生成：</strong>自動產生唯一學生 ID</li>
                <li><strong>表單重置：</strong>新增後清空表單內容</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>使用 v-model 綁定表單資料</li>
                <li>實作 addStudent 方法處理新增邏輯</li>
                <li>加入表單驗證機制</li>
                <li>生成唯一 ID 並加入學生陣列</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">3.</span>
            <span class="function-name">統計資料計算</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            使用計算屬性實作學生成績的各項統計功能
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>總學生數：</strong>計算學生陣列長度</li>
                <li><strong>及格人數：</strong>統計分數 >= 60 的學生數量</li>
                <li><strong>平均分數：</strong>計算所有學生分數平均值</li>
                <li><strong>即時更新：</strong>資料變化時自動重新計算</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作 totalStudents 計算屬性</li>
                <li>實作 passedCount 計算屬性（分數 >= 60）</li>
                <li>實作 averageScore 計算屬性（保留一位小數）</li>
                <li>處理空陣列的邊界情況</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">4.</span>
            <span class="function-name">編輯學生資料</span>
            <span class="difficulty hard">困難</span>
          </div>
          <div class="function-description">
            實作學生資料的編輯功能，包含狀態管理和資料同步
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>編輯模式：</strong>點擊編輯按鈕進入編輯狀態</li>
                <li><strong>資料複製：</strong>避免直接修改原始物件</li>
                <li><strong>儲存功能：</strong>驗證後更新學生資料</li>
                <li><strong>取消功能：</strong>恢復原始狀態不儲存變更</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作 editStudent 方法設定編輯狀態</li>
                <li>使用 editingId 追蹤當前編輯的學生</li>
                <li>實作 saveEdit 方法儲存變更</li>
                <li>實作 cancelEdit 方法取消編輯</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">5.</span>
            <span class="function-name">篩選與排序</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            實作動態資料篩選和排序功能，提升使用者體驗
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>篩選條件：</strong>切換顯示全部或僅及格學生</li>
                <li><strong>排序功能：</strong>按分數高低排序</li>
                <li><strong>計算屬性：</strong>使用 filteredStudents 動態篩選</li>
                <li><strong>狀態切換：</strong>按鈕文字隨狀態改變</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作 filteredStudents 計算屬性</li>
                <li>根據 showPassed 狀態篩選學生</li>
                <li>實作 sortByScore 排序方法</li>
                <li>實作刪除學生功能</li>
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
              <strong>資料結構</strong>
              <p>先建立學生資料陣列和表單資料結構</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">2</div>
            <div class="step-content">
              <strong>基本渲染</strong>
              <p>使用 v-for 實作學生列表的基本顯示</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">3</div>
            <div class="step-content">
              <strong>統計功能</strong>
              <p>實作各項統計計算屬性</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">4</div>
            <div class="step-content">
              <strong>互動功能</strong>
              <p>加入新增、編輯、刪除、篩選功能</p>
            </div>
          </div>
        </div>
      </div>

      <div class="hint-section">
        <h4>💡 開發提示</h4>
        <details>
          <summary>點擊查看開發提示</summary>
          <div class="hints">
            <h5>v-for 使用要點：</h5>
            <ul>
              <li><strong>key 屬性：</strong>必須為每個項目提供唯一的 key</li>
              <li><strong>陣列索引：</strong>避免使用 index 作為 key（會影響效能）</li>
              <li><strong>計算屬性：</strong>用於動態篩選和排序資料</li>
              <li><strong>響應式更新：</strong>確保陣列變更能觸發畫面更新</li>
            </ul>

            <h5>常見問題解決：</h5>
            <ul>
              <li><strong>列表不更新：</strong>檢查是否正確使用響應式方法</li>
              <li><strong>key 警告：</strong>確保每個 v-for 項目都有唯一 key</li>
              <li><strong>編輯衝突：</strong>使用物件深拷貝避免直接修改原始資料</li>
              <li><strong>計算錯誤：</strong>處理空陣列和無效數值的邊界情況</li>
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
  border-left: 5px solid #007bff;
}

.challenge-section h3 {
  color: #007bff;
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
  accent-color: #007bff;
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
