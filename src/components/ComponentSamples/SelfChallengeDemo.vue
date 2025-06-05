<template>
  <div class="self-challenge-container">
    <!-- 標題區域 -->
    <div class="header">
      <h2>🧩 組件化自我試煉</h2>
      <p class="file-path">📁 src/components/ComponentSamples/SelfChallengeDemo.vue</p>
    </div>

    <!-- 挑戰清單 -->
    <div class="challenge-list">
      <h3>🎯 挑戰任務清單</h3>
      <ul>
        <li>⭕ 創建 TaskItem 子組件，接收 props</li>
        <li>⭕ 實現父子組件通信（emit 事件）</li>
        <li>⭕ 使用插槽（slot）自定義內容</li>
        <li>⭕ 實現組件間數據傳遞</li>
        <li>⭕ 創建可重用的 UI 組件</li>
        <li>⭕ 組件生命週期管理</li>
      </ul>
    </div>

    <!-- 演示區域 -->
    <div class="demo-section">
      <h3>📋 任務管理系統</h3>

      <!-- 任務統計卡片 -->
      <div class="stats-grid">
        <!-- TODO: 使用 StatsCard 組件顯示統計資料 -->
        <!-- 提示：傳遞 title, value, color 等 props -->

      </div>

      <!-- 新增任務表單 -->
      <div class="add-task-form">
        <!-- TODO: 使用 TaskForm 組件 -->
        <!-- 提示：監聽 @add-task 事件 -->

      </div>

      <!-- 任務篩選器 -->
      <div class="task-filters">
        <!-- TODO: 使用 TaskFilter 組件 -->
        <!-- 提示：綁定 v-model 和監聽篩選事件 -->

      </div>

      <!-- 任務列表 -->
      <div class="task-list">
        <!-- TODO: 使用 v-for 渲染 TaskItem 組件 -->
        <!-- 提示：傳遞 task props，監聽各種事件 -->

      </div>

      <!-- 空狀態組件 -->
      <div v-if="filteredTasks.length === 0" class="empty-state">
        <!-- TODO: 使用 EmptyState 組件 -->

      </div>
    </div>

    <!-- 任務詳情模態框 -->
    <div v-if="selectedTask" class="modal-overlay" @click="closeTaskDetails">
      <div class="modal-content" @click.stop>
        <!-- TODO: 使用 TaskDetail 組件 -->

      </div>
    </div>

    <!-- 提示區域 -->
    <div class="hints-section">
      <h3>💡 實作提示</h3>
      <div class="hints-grid">
        <div class="hint-card">
          <h4>Props 傳遞</h4>
          <p>使用 defineProps() 定義組件接收的屬性</p>
          <code>const props = defineProps(['task', 'color'])</code>
        </div>
        <div class="hint-card">
          <h4>事件發射</h4>
          <p>使用 defineEmits() 定義組件發出的事件</p>
          <code>const emit = defineEmits(['add-task', 'delete-task'])</code>
        </div>
        <div class="hint-card">
          <h4>插槽使用</h4>
          <p>使用 &lt;slot&gt; 標籤定義可插入內容的位置</p>
          <code>&lt;slot name="actions"&gt;&lt;/slot&gt;</code>
        </div>
        <div class="hint-card">
          <h4>組件註冊</h4>
          <p>在 script setup 中導入子組件</p>
          <code>import TaskItem from './components/TaskItem.vue'</code>
        </div>
      </div>
    </div>

    <!-- 練習詳情區域 -->
    <div class="practice-details">
      <h3>📚 學員需要自己完成的練習</h3>

      <!-- 實作步驟指南 -->
      <div class="implementation-guide">
        <h4>🚀 實作步驟指南</h4>
        <p class="guide-intro">按照以下步驟完成組件化任務管理系統的實作：</p>

        <!-- 步驟1: 創建目錄結構 -->
        <div class="step-section">
          <h5>📁 步驟 1: 創建目錄結構</h5>
          <p>在 <code>src/components/ComponentSamples/components/SelfChallenge/</code> 下創建 <code>SelfChallenge</code>
            資料夾，並建立以下檔案：</p>
          <ul class="file-list">
            <li>📄 TaskItem.vue</li>
            <li>📄 TaskForm.vue</li>
            <li>📄 TaskFilter.vue</li>
            <li>📄 StatsCard.vue</li>
            <li>📄 EmptyState.vue</li>
            <li>📄 TaskDetail.vue</li>
          </ul>
        </div>

        <!-- 步驟2: 主組件功能實作 -->
        <div class="step-section">
          <h5>🏠 步驟 2: 主組件功能實作</h5>

          <div class="implementation-item">
            <h6>🧮 計算屬性實作邏輯</h6>
            <div class="logic-description">
              <p><strong>completedCount：</strong></p>
              <ul>
                <li>使用 tasks.value.filter() 篩選 completed 為 true 的任務</li>
                <li>回傳篩選結果的 length 屬性</li>
              </ul>

              <p><strong>pendingCount：</strong></p>
              <ul>
                <li>使用 tasks.value.filter() 篩選 completed 為 false 的任務</li>
                <li>回傳篩選結果的 length 屬性</li>
              </ul>

              <p><strong>completionRate：</strong></p>
              <ul>
                <li>如果 tasks.value.length 為 0，回傳 0</li>
                <li>否則計算 (completedCount.value / tasks.value.length) * 100</li>
                <li>使用 Math.round() 四捨五入到整數</li>
              </ul>

              <p><strong>filteredTasks：</strong></p>
              <ul>
                <li>使用 switch 語句根據 currentFilter.value 的值進行篩選</li>
                <li>'all': 回傳 tasks.value</li>
                <li>'completed': 篩選 completed 為 true 的任務</li>
                <li>'pending': 篩選 completed 為 false 的任務</li>
                <li>'high', 'medium', 'low': 根據 priority 屬性篩選</li>
              </ul>
            </div>
          </div>

          <div class="implementation-item">
            <h6>🎯 事件處理方法邏輯</h6>
            <div class="logic-description">
              <p><strong>handleAddTask：</strong></p>
              <ul>
                <li>接收 newTask 參數</li>
                <li>建立新物件：id (使用 Date.now())、...newTask、completed: false、createdAt: new Date()</li>
                <li>將新任務 push 到 tasks.value 陣列</li>
              </ul>

              <p><strong>handleToggleComplete：</strong></p>
              <ul>
                <li>接收 taskId 參數</li>
                <li>使用 findIndex() 找到對應任務的索引</li>
                <li>如果找到，切換該任務的 completed 狀態</li>
              </ul>

              <p><strong>handleDeleteTask：</strong></p>
              <ul>
                <li>接收 taskId 參數</li>
                <li>使用 filter() 過濾掉指定 id 的任務</li>
                <li>更新 tasks.value</li>
              </ul>

              <p><strong>handleFilterChange：</strong></p>
              <ul>
                <li>接收 filter 參數</li>
                <li>將 currentFilter.value 設為接收的值</li>
              </ul>

              <p><strong>showTaskDetails：</strong></p>
              <ul>
                <li>接收 task 參數</li>
                <li>將 selectedTask.value 設為該任務物件</li>
              </ul>
            </div>
          </div>

          <div class="implementation-item">
            <h6>🏗️ 子組件使用方式</h6>
            <div class="component-usage">
              <p><strong>StatsCard 組件：</strong>在 stats-grid 區域使用，需傳遞 title、value、color、icon props</p>
              <p><strong>TaskForm 組件：</strong>在 add-task-form 區域使用，監聽 add-task 事件</p>
              <p><strong>TaskFilter 組件：</strong>在 task-filters 區域使用，使用 v-model 綁定 currentFilter</p>
              <p><strong>TaskItem 組件：</strong>在 task-list 區域使用 v-for 迴圈渲染，監聽各種事件</p>
              <p><strong>EmptyState 組件：</strong>在 empty-state 區域使用，配置具名插槽</p>
              <p><strong>TaskDetail 組件：</strong>在 modal-content 區域使用，傳遞 task prop</p>
            </div>
          </div>
        </div>

        <!-- 步驟3: 子組件實作規格 -->
        <div class="step-section">
          <h5>🧩 步驟 3: 子組件實作規格</h5>

          <div class="component-spec-grid">
            <div class="spec-card">
              <h6>📋 TaskItem.vue</h6>
              <div class="spec-content">
                <p><strong>Props：</strong>task (Object, required)</p>
                <p><strong>Events：</strong>toggle-complete, delete-task, edit-task, show-details</p>
                <p><strong>功能：</strong></p>
                <ul>
                  <li>顯示任務資訊（標題、描述、分類、日期）</li>
                  <li>優先級標籤顯示（high/medium/low → 高/中/低）</li>
                  <li>日期格式化（使用 toLocaleDateString）</li>
                  <li>過期狀態檢查（dueDate &lt; 當前日期且未完成）</li>
                  <li>操作按鈕（完成、編輯、刪除、詳情）</li>
                  <li>具名插槽支援自定義操作按鈕</li>
                </ul>
              </div>
            </div>

            <div class="spec-card">
              <h6>📝 TaskForm.vue</h6>
              <div class="spec-content">
                <p><strong>Events：</strong>add-task</p>
                <p><strong>功能：</strong></p>
                <ul>
                  <li>表單欄位：title, description, priority, category, dueDate</li>
                  <li>表單驗證：標題必填、長度限制、日期不能早於今天</li>
                  <li>錯誤訊息顯示</li>
                  <li>提交後重置表單</li>
                  <li>載入狀態處理</li>
                </ul>
              </div>
            </div>

            <div class="spec-card">
              <h6>🔍 TaskFilter.vue</h6>
              <div class="spec-content">
                <p><strong>Props：</strong>modelValue (String, default: 'all')</p>
                <p><strong>Events：</strong>update:modelValue, filter-change</p>
                <p><strong>功能：</strong></p>
                <ul>
                  <li>篩選選項：全部、已完成、待完成、高/中/低優先級</li>
                  <li>v-model 雙向綁定實現</li>
                  <li>活躍狀態顯示</li>
                  <li>重置篩選功能</li>
                </ul>
              </div>
            </div>

            <div class="spec-card">
              <h6>📊 StatsCard.vue</h6>
              <div class="spec-content">
                <p><strong>Props：</strong>title, value, icon, color, progress</p>
                <p><strong>功能：</strong></p>
                <ul>
                  <li>數值格式化顯示（千分位分隔）</li>
                  <li>多種顏色主題（blue, green, orange, purple, red）</li>
                  <li>進度條顯示（可選）</li>
                  <li>動態樣式計算</li>
                  <li>Props 驗證規則</li>
                </ul>
              </div>
            </div>

            <div class="spec-card">
              <h6>🗂️ EmptyState.vue</h6>
              <div class="spec-content">
                <p><strong>Props：</strong>size (可選)</p>
                <p><strong>功能：</strong></p>
                <ul>
                  <li>具名插槽：icon, title, description, actions</li>
                  <li>預設內容提供</li>
                  <li>多種尺寸支援</li>
                  <li>靈活的插槽組合</li>
                </ul>
              </div>
            </div>

            <div class="spec-card">
              <h6>🔍 TaskDetail.vue</h6>
              <div class="spec-content">
                <p><strong>Props：</strong>task</p>
                <p><strong>Events：</strong>update-task, close</p>
                <p><strong>功能：</strong></p>
                <ul>
                  <li>詳情檢視/編輯模式切換</li>
                  <li>編輯表單處理</li>
                  <li>資料更新邏輯</li>
                  <li>取消編輯功能</li>
                </ul>
              </div>
            </div>
          </div>
        </div>

        <!-- 步驟4: 實作提示 -->
        <div class="step-section">
          <h5>💡 步驟 4: 核心技術實作要點</h5>
          <div class="tips-grid">
            <div class="tip-card">
              <h6>📦 組件檔案結構</h6>
              <p><strong>路徑：</strong> src/components/ComponentSamples/components/SelfChallenge/</p>
              <p><strong>命名：</strong> 使用 PascalCase (如 TaskItem.vue)</p>
              <p><strong>導入：</strong> import ComponentName from './SelfChallenge/ComponentName.vue'</p>
            </div>
            <div class="tip-card">
              <h6>🔧 Props 設計原則</h6>
              <p><strong>類型驗證：</strong> 使用 type、required、validator 屬性</p>
              <p><strong>預設值：</strong> 為非必要 props 提供合理預設值</p>
              <p><strong>文檔化：</strong> 為每個 prop 添加註解說明用途</p>
            </div>
            <div class="tip-card">
              <h6>📡 事件命名規範</h6>
              <p><strong>格式：</strong> 使用 kebab-case (如 add-task)</p>
              <p><strong>語意：</strong> 動詞+名詞組合，表達清晰的動作</p>
              <p><strong>載體：</strong> 事件攜帶必要的數據參數</p>
            </div>
            <div class="tip-card">
              <h6>🔄 v-model 實現邏輯</h6>
              <p><strong>接收：</strong> modelValue props (可自訂名稱)</p>
              <p><strong>發射：</strong> update:modelValue 事件</p>
              <p><strong>計算：</strong> 使用 computed 的 get/set 簡化操作</p>
            </div>
            <div class="tip-card">
              <h6>🎯 插槽設計策略</h6>
              <p><strong>預設插槽：</strong> 提供基本內容佔位</p>
              <p><strong>具名插槽：</strong> 允許特定區域自定義</p>
              <p><strong>作用域插槽：</strong> 傳遞內部數據給父組件</p>
            </div>
            <div class="tip-card">
              <h6>🧮 響應式數據管理</h6>
              <p><strong>ref：</strong> 基本數據類型和物件引用</p>
              <p><strong>reactive：</strong> 深層響應式物件</p>
              <p><strong>computed：</strong> 基於其他響應式數據的衍生狀態</p>
            </div>
            <div class="tip-card">
              <h6>🎨 CSS 樣式組織</h6>
              <p><strong>scoped：</strong> 使用 scoped 避免樣式污染</p>
              <p><strong>BEM：</strong> 採用 BEM 命名規範增強可讀性</p>
              <p><strong>變數：</strong> 定義 CSS 變數統一主題色彩</p>
            </div>
            <div class="tip-card">
              <h6>🛠️ 開發工具提示</h6>
              <p><strong>Vue DevTools：</strong> 使用開發者工具調試組件</p>
              <p><strong>ESLint：</strong> 遵循程式碼品質檢查規則</p>
              <p><strong>TypeScript：</strong> 可選加入類型檢查支援</p>
            </div>
            <div class="tip-card">
              <h6>⚡ 效能優化建議</h6>
              <p><strong>v-memo：</strong> 對大列表使用記憶化優化</p>
              <p><strong>懶加載：</strong> 大組件可考慮動態導入</p>
              <p><strong>事件綁定：</strong> 避免在模板中使用匿名函數</p>
            </div>
            <div class="tip-card">
              <h6>🔍 除錯技巧</h6>
              <p><strong>console.log：</strong> 在關鍵位置輸出狀態資訊</p>
              <p><strong>watch：</strong> 監控響應式數據的變化</p>
              <p><strong>錯誤邊界：</strong> 使用 errorCaptured 處理錯誤</p>
            </div>
            <div class="tip-card">
              <h6>📚 學習資源建議</h6>
              <p><strong>官方文檔：</strong> vuejs.org 是最權威的參考</p>
              <p><strong>範例專案：</strong> 參考優秀的開源 Vue 專案</p>
              <p><strong>社群討論：</strong> Stack Overflow、Vue 中文社群</p>
            </div>
            <div class="tip-card">
              <h6>🎯 實作順序建議</h6>
              <p><strong>1. 靜態結構：</strong> 先建立 HTML 模板結構</p>
              <p><strong>2. 資料流動：</strong> 再實作 props 和事件</p>
              <p><strong>3. 互動功能：</strong> 最後加入動態行為邏輯</p>
            </div>
          </div>
        </div>
      </div>

      <!-- 詳細實作規格 -->
      <div class="detailed-specs">
        <h4>🔧 完整實作評估清單</h4>
        <p class="specs-intro">學員需要完成以下所有功能才算完成練習：</p>

        <!-- 主組件評估清單 -->
        <div class="checklist-section">
          <h5>✅ 主組件完成清單</h5>

          <div class="checklist-group">
            <h6>📦 組件導入 (必須完成)</h6>
            <ul class="checklist">
              <li>創建 SelfChallenge 資料夾</li>
              <li>導入 TaskItem 組件</li>
              <li>導入 TaskForm 組件</li>
              <li>導入 TaskFilter 組件</li>
              <li>導入 StatsCard 組件</li>
              <li>導入 EmptyState 組件</li>
              <li>導入 TaskDetail 組件</li>
            </ul>
          </div>

          <div class="checklist-group">
            <h6>🧮 計算屬性實作 (必須完成)</h6>
            <ul class="checklist">
              <li>completedCount: 使用 filter 計算已完成任務數量</li>
              <li>pendingCount: 使用 filter 計算待完成任務數量</li>
              <li>completionRate: 計算完成率百分比 (0-100)</li>
              <li>filteredTasks: 根據 currentFilter 篩選任務</li>
            </ul>
          </div>

          <div class="checklist-group">
            <h6>🎯 事件處理方法 (必須完成)</h6>
            <ul class="checklist">
              <li>handleAddTask: 新增任務到陣列 (生成ID、設定預設值)</li>
              <li>handleToggleComplete: 切換任務完成狀態</li>
              <li>handleDeleteTask: 從陣列中移除任務</li>
              <li>handleEditTask: 更新任務資料</li>
              <li>handleFilterChange: 更新篩選條件</li>
              <li>showTaskDetails: 設定選中任務</li>
              <li>handleUpdateTask: 處理任務更新</li>
            </ul>
          </div>

          <div class="checklist-group">
            <h6>🏗️ 模板組件使用 (必須完成)</h6>
            <ul class="checklist">
              <li>在 stats-grid 使用 4 個 StatsCard 組件</li>
              <li>在 add-task-form 使用 TaskForm 組件</li>
              <li>在 task-filters 使用 TaskFilter 組件</li>
              <li>在 task-list 使用 v-for 渲染 TaskItem</li>
              <li>在 empty-state 使用 EmptyState 組件</li>
              <li>在 modal-content 使用 TaskDetail 組件</li>
            </ul>
          </div>
        </div>

        <!-- 子組件評估清單 -->
        <div class="checklist-section">
          <h5>✅ 子組件完成清單</h5>

          <div class="component-checklist">
            <h6>📋 TaskItem.vue</h6>
            <ul class="checklist">
              <li>定義 task props (Object, required, 含驗證)</li>
              <li>定義 4 個 emits 事件</li>
              <li>實作 priorityText 計算屬性 (高/中/低)</li>
              <li>實作 formattedDate 計算屬性</li>
              <li>實作 isOverdue 計算屬性</li>
              <li>4 個事件處理方法</li>
              <li>完整模板結構含插槽</li>
            </ul>
          </div>

          <div class="component-checklist">
            <h6>📝 TaskForm.vue</h6>
            <ul class="checklist">
              <li>響應式表單資料 (5個欄位)</li>
              <li>錯誤狀態管理</li>
              <li>提交狀態管理</li>
              <li>完整表單驗證邏輯</li>
              <li>提交處理方法</li>
              <li>表單重置方法</li>
              <li>發射 add-task 事件</li>
            </ul>
          </div>

          <div class="component-checklist">
            <h6>🔍 TaskFilter.vue</h6>
            <ul class="checklist">
              <li>modelValue props 定義</li>
              <li>定義 2 個 emits 事件</li>
              <li>v-model 雙向綁定實現</li>
              <li>篩選選項陣列定義</li>
              <li>活躍狀態判斷方法</li>
              <li>重置篩選方法</li>
            </ul>
          </div>

          <div class="component-checklist">
            <h6>📊 StatsCard.vue</h6>
            <ul class="checklist">
              <li>5 個 props 定義含驗證</li>
              <li>動態樣式計算屬性</li>
              <li>數值格式化計算屬性</li>
              <li>進度條樣式計算屬性</li>
              <li>多主題顏色支援</li>
            </ul>
          </div>

          <div class="component-checklist">
            <h6>🗂️ EmptyState.vue</h6>
            <ul class="checklist">
              <li>4 個具名插槽實現</li>
              <li>預設插槽內容</li>
              <li>可選 size props</li>
              <li>彈性插槽組合</li>
            </ul>
          </div>

          <div class="component-checklist">
            <h6>🔍 TaskDetail.vue</h6>
            <ul class="checklist">
              <li>task props 定義</li>
              <li>2 個 emits 事件定義</li>
              <li>編輯狀態管理</li>
              <li>編輯表單資料</li>
              <li>開始編輯方法</li>
              <li>儲存編輯方法</li>
              <li>取消編輯方法</li>
            </ul>
          </div>
        </div>

        <!-- 測試驗證 -->
        <div class="testing-section">
          <h5>🧪 功能測試驗證</h5>
          <div class="test-grid">
            <div class="test-item">
              <h6>基本功能測試</h6>
              <ul>
                <li>新增任務功能正常</li>
                <li>任務列表正確顯示</li>
                <li>完成狀態切換正常</li>
                <li>刪除任務功能正常</li>
              </ul>
            </div>
            <div class="test-item">
              <h6>篩選功能測試</h6>
              <ul>
                <li>全部任務篩選</li>
                <li>已完成篩選</li>
                <li>待完成篩選</li>
                <li>優先級篩選</li>
              </ul>
            </div>
            <div class="test-item">
              <h6>統計功能測試</h6>
              <ul>
                <li>總任務數正確</li>
                <li>已完成數正確</li>
                <li>待完成數正確</li>
                <li>完成率正確</li>
              </ul>
            </div>
            <div class="test-item">
              <h6>進階功能測試</h6>
              <ul>
                <li>任務詳情顯示</li>
                <li>編輯任務功能</li>
                <li>表單驗證正常</li>
                <li>空狀態顯示</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- 子組件練習 -->
    <div class="practice-section">
      <h4>2️⃣ 子組件練習</h4>
      <div class="practice-grid">
        <div class="component-practice">
          <h5>📋 TaskItem</h5>
          <p><strong>重點：</strong>Props 定義、事件發射、插槽使用</p>
          <ul>
            <li>定義 task prop 接收任務資料</li>
            <li>發射 toggle-complete、delete-task、edit-task 事件</li>
            <li>使用具名插槽允許自定義操作按鈕</li>
            <li>實作優先級文字轉換</li>
            <li>實作日期格式化顯示</li>
          </ul>
        </div>

        <div class="component-practice">
          <h5>📝 TaskForm</h5>
          <p><strong>重點：</strong>表單處理、v-model 綁定、驗證邏輯</p>
          <ul>
            <li>使用 v-model 綁定所有表單欄位</li>
            <li>實作表單驗證邏輯</li>
            <li>發射 add-task 事件</li>
            <li>實作表單重置功能</li>
            <li>顯示表單預覽和錯誤訊息</li>
          </ul>
        </div>

        <div class="component-practice">
          <h5>🔍 TaskFilter</h5>
          <p><strong>重點：</strong>v-model 實現、計算屬性、事件處理</p>
          <ul>
            <li>實現 v-model 雙向綁定</li>
            <li>處理多種篩選條件</li>
            <li>發射 filter-change 事件</li>
            <li>計算活躍篩選狀態</li>
            <li>實作篩選重置功能</li>
          </ul>
        </div>

        <div class="component-practice">
          <h5>📊 StatsCard</h5>
          <p><strong>重點：</strong>Props 驗證、計算屬性、動態樣式</p>
          <ul>
            <li>定義多種 props 和驗證規則</li>
            <li>實作數值格式化顯示</li>
            <li>根據 props 計算圖標和樣式</li>
            <li>實作進度條百分比計算</li>
            <li>支援多種顏色主題</li>
          </ul>
        </div>

        <div class="component-practice">
          <h5>🗂️ EmptyState</h5>
          <p><strong>重點：</strong>插槽系統使用</p>
          <ul>
            <li>使用具名插槽（icon、title、description）</li>
            <li>提供預設插槽內容</li>
            <li>支援多種插槽組合</li>
            <li>理解插槽的靈活性</li>
          </ul>
        </div>

        <div class="component-practice">
          <h5>🔍 TaskDetail</h5>
          <p><strong>重點：</strong>複雜組件邏輯、編輯模式</p>
          <ul>
            <li>實作編輯/檢視模式切換</li>
            <li>處理複雜的事件邏輯</li>
            <li>實作表單驗證和更新</li>
            <li>使用插槽自定義操作</li>
          </ul>
        </div>
      </div>
    </div>

    <!-- 學習目標 -->
    <div class="learning-goals">
      <h4>🎯 學習目標</h4>
      <div class="goals-grid">
        <div class="goal-item">
          <span class="goal-icon">📡</span>
          <span class="goal-text">掌握組件間通信（Props 下傳、Events 上傳）</span>
        </div>
        <div class="goal-item">
          <span class="goal-icon">🔧</span>
          <span class="goal-text">熟練使用插槽系統（具名插槽、作用域插槽）</span>
        </div>
        <div class="goal-item">
          <span class="goal-icon">🔄</span>
          <span class="goal-text">理解 v-model 雙向綁定在組件中的實現</span>
        </div>
        <div class="goal-item">
          <span class="goal-icon">🧩</span>
          <span class="goal-text">學會設計可重用的 UI 組件</span>
        </div>
        <div class="goal-item">
          <span class="goal-icon">⚡</span>
          <span class="goal-text">掌握組件生命週期和響應式系統</span>
        </div>
        <div class="goal-item">
          <span class="goal-icon">🏗️</span>
          <span class="goal-text">建立完整的組件化應用架構</span>
        </div>
      </div>
    </div>
  </div>

</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

// TODO: 導入所有需要的子組件
// 提示：import TaskItem from './components/SelfChallenge/TaskItem.vue'

// 響應式數據
const tasks = ref([
  {
    id: 1,
    title: '學習 Vue3 組件化',
    description: '掌握 props、emit、slot 等核心概念',
    priority: 'high',
    category: '學習',
    completed: false,
    createdAt: new Date('2024-01-15'),
    dueDate: new Date('2024-01-20')
  },
  {
    id: 2,
    title: '完成專案文檔',
    description: '撰寫 API 文檔和使用說明',
    priority: 'medium',
    category: '工作',
    completed: true,
    createdAt: new Date('2024-01-10'),
    dueDate: new Date('2024-01-18')
  },
  {
    id: 3,
    title: '準備技術分享',
    description: '準備 Vue3 最佳實踐分享內容',
    priority: 'low',
    category: '分享',
    completed: false,
    createdAt: new Date('2024-01-12'),
    dueDate: new Date('2024-01-25')
  }
])

const currentFilter = ref('all')
const selectedTask = ref(null)

// TODO: 實現計算屬性
// 提示：計算已完成任務數量、待完成數量、完成率等
const completedCount = computed(() => {
  // TODO: 計算已完成的任務數量
  return 0
})

const pendingCount = computed(() => {
  // TODO: 計算待完成的任務數量
  return 0
})

const completionRate = computed(() => {
  // TODO: 計算完成率百分比
  return 0
})

const filteredTasks = computed(() => {
  // TODO: 根據當前篩選條件過濾任務
  return tasks.value
})

// TODO: 實現事件處理方法
const handleAddTask = (newTask) => {
  // TODO: 添加新任務到列表
  console.log('新增任務:', newTask)
}

const handleToggleComplete = (taskId) => {
  // TODO: 切換任務完成狀態
  console.log('切換完成狀態:', taskId)
}

const handleDeleteTask = (taskId) => {
  // TODO: 刪除指定任務
  console.log('刪除任務:', taskId)
}

const handleEditTask = (taskId, updatedData) => {
  // TODO: 編輯任務資料
  console.log('編輯任務:', taskId, updatedData)
}

const handleFilterChange = (filter) => {
  // TODO: 處理篩選條件變更
  console.log('篩選變更:', filter)
}

const showTaskDetails = (task) => {
  // TODO: 顯示任務詳情
  console.log('顯示詳情:', task)
}

const closeTaskDetails = () => {
  // TODO: 關閉任務詳情
  selectedTask.value = null
}

const handleUpdateTask = (updatedTask) => {
  // TODO: 更新任務資料
  console.log('更新任務:', updatedTask)
}

// 生命週期
onMounted(() => {
  console.log('任務管理系統已載入')
  // TODO: 可以在這裡載入儲存的任務資料
})
</script>

<style scoped>
.self-challenge-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.header {
  text-align: center;
  margin-bottom: 30px;
  padding: 20px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border-radius: 15px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
}

.header h2 {
  margin: 0 0 10px 0;
  font-size: 2.5em;
  font-weight: 700;
}

.file-path {
  margin: 0;
  opacity: 0.9;
  font-size: 0.9em;
  font-family: 'Courier New', monospace;
}

.challenge-list {
  background: #f8f9ff;
  padding: 25px;
  border-radius: 15px;
  margin-bottom: 30px;
  border-left: 5px solid #667eea;
}

.challenge-list h3 {
  color: #333;
  margin-bottom: 15px;
  font-size: 1.3em;
}

.challenge-list ul {
  list-style: none;
  padding: 0;
}

.challenge-list li {
  padding: 8px 0;
  font-size: 1.1em;
  color: #555;
}

.demo-section {
  background: white;
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.08);
  margin-bottom: 30px;
}

.demo-section h3 {
  color: #333;
  margin-bottom: 25px;
  font-size: 1.5em;
  text-align: center;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
  margin-bottom: 30px;
}

.add-task-form {
  margin-bottom: 25px;
  padding: 20px;
  background: #f8f9fa;
  border-radius: 10px;
}

.task-filters {
  margin-bottom: 25px;
}

.task-list {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.empty-state {
  text-align: center;
  padding: 40px;
  color: #666;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal-content {
  background: white;
  border-radius: 15px;
  max-width: 600px;
  width: 90%;
  max-height: 80vh;
  overflow-y: auto;
}

.hints-section {
  background: #fff3cd;
  padding: 25px;
  border-radius: 15px;
  border-left: 5px solid #ffc107;
}

.hints-section h3 {
  color: #856404;
  margin-bottom: 20px;
  font-size: 1.3em;
}

.hints-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
}

.hint-card {
  background: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.hint-card h4 {
  color: #495057;
  margin-bottom: 10px;
  font-size: 1.1em;
}

.hint-card p {
  color: #6c757d;
  margin-bottom: 10px;
  line-height: 1.5;
}

.hint-card code {
  background: #f8f9fa;
  padding: 8px 12px;
  border-radius: 5px;
  font-family: 'Courier New', monospace;
  font-size: 0.9em;
  color: #e83e8c;
  display: block;
  overflow-x: auto;
}

.btn {
  padding: 8px 16px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 0.9em;
  transition: all 0.3s ease;
}

.btn-sm {
  padding: 6px 12px;
  font-size: 0.8em;
}

.btn-info {
  background: #17a2b8;
  color: white;
}

.btn-info:hover {
  background: #138496;
  transform: translateY(-1px);
}

@media (max-width: 768px) {
  .self-challenge-container {
    padding: 15px;
  }

  .header h2 {
    font-size: 2em;
  }

  .stats-grid {
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 15px;
  }

  .hints-grid {
    grid-template-columns: 1fr;
    gap: 15px;
  }
}

.practice-details {
  background: #f0f8ff;
  padding: 30px;
  border-radius: 15px;
  margin-top: 30px;
  border: 2px solid #e3f2fd;
}

.practice-details h3 {
  color: #1565c0;
  margin-bottom: 25px;
  font-size: 1.5em;
  text-align: center;
}

.practice-section {
  margin-bottom: 35px;
  background: white;
  padding: 25px;
  border-radius: 12px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
}

.practice-section h4 {
  color: #333;
  margin-bottom: 20px;
  font-size: 1.3em;
  border-bottom: 2px solid #e3f2fd;
  padding-bottom: 10px;
}

.practice-list {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.practice-item {
  background: #fafafa;
  padding: 20px;
  border-radius: 10px;
  border-left: 4px solid #2196f3;
}

.practice-item h5 {
  color: #1565c0;
  margin: 0 0 15px 0;
  font-size: 1.1em;
}

.practice-item ul {
  margin: 0;
  padding-left: 20px;
}

.practice-item li {
  margin: 8px 0;
  color: #555;
  line-height: 1.5;
}

.practice-item code {
  background: #e8f5e9;
  padding: 2px 6px;
  border-radius: 4px;
  font-family: 'Courier New', monospace;
  color: #2e7d32;
  font-size: 0.9em;
}

.practice-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 20px;
}

.component-practice {
  background: #f8f9fa;
  padding: 20px;
  border-radius: 10px;
  border: 1px solid #dee2e6;
}

.component-practice h5 {
  color: #495057;
  margin: 0 0 10px 0;
  font-size: 1.1em;
}

.component-practice p {
  margin: 0 0 15px 0;
  color: #6c757d;
  font-size: 0.9em;
}

.component-practice ul {
  margin: 0;
  padding-left: 20px;
}

.component-practice li {
  margin: 6px 0;
  color: #495057;
  font-size: 0.9em;
  line-height: 1.4;
}

.learning-goals {
  background: #fff8e1;
  padding: 25px;
  border-radius: 12px;
  border: 2px solid #ffcc02;
}

.learning-goals h4 {
  color: #e65100;
  margin: 0 0 20px 0;
  font-size: 1.3em;
  text-align: center;
}

.goals-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 15px;
}

.goal-item {
  display: flex;
  align-items: center;
  gap: 12px;
  background: white;
  padding: 15px;
  border-radius: 8px;
  box-shadow: 0 1px 5px rgba(0, 0, 0, 0.1);
}

.goal-icon {
  font-size: 1.5em;
  flex-shrink: 0;
}

.goal-text {
  color: #424242;
  font-size: 0.95em;
  line-height: 1.4;
}

/* 實作步驟指南樣式 */
.implementation-guide {
  background: #e8f5e9;
  padding: 25px;
  border-radius: 15px;
  margin-bottom: 30px;
  border-left: 5px solid #4caf50;
}

.implementation-guide h4 {
  color: #2e7d32;
  margin-bottom: 15px;
  font-size: 1.3em;
}

.guide-intro {
  color: #424242;
  margin-bottom: 25px;
  font-size: 1.05em;
  line-height: 1.6;
}

.step-section {
  background: white;
  padding: 25px;
  border-radius: 12px;
  margin-bottom: 25px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
}

.step-section h5 {
  color: #1976d2;
  margin-bottom: 20px;
  font-size: 1.2em;
  border-bottom: 2px solid #e3f2fd;
  padding-bottom: 10px;
}

.file-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 10px;
  list-style: none;
  padding: 0;
  margin: 15px 0;
}

.file-list li {
  background: #f5f5f5;
  padding: 10px 15px;
  border-radius: 8px;
  font-family: 'Courier New', monospace;
  border-left: 3px solid #2196f3;
}

.implementation-item {
  margin-bottom: 25px;
  padding: 20px;
  background: #fafafa;
  border-radius: 10px;
  border-left: 4px solid #ff9800;
}

.implementation-item h6 {
  color: #e65100;
  margin: 0 0 15px 0;
  font-size: 1.1em;
}

.logic-description {
  margin-top: 10px;
}

.logic-description p {
  margin: 10px 0 5px 0;
  font-weight: 600;
  color: #424242;
}

.logic-description ul {
  margin: 5px 0 15px 20px;
  padding: 0;
}

.logic-description li {
  margin: 5px 0;
  color: #555;
  line-height: 1.4;
}

.component-usage p {
  margin: 8px 0;
  padding: 10px;
  background: #fff3e0;
  border-radius: 6px;
  border-left: 3px solid #ff9800;
  color: #e65100;
}

.component-spec-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 20px;
  margin-top: 20px;
}

.spec-card {
  background: white;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.08);
  border: 1px solid #e0e0e0;
}

.spec-card h6 {
  color: #1976d2;
  margin: 0 0 15px 0;
  font-size: 1.1em;
  padding-bottom: 8px;
  border-bottom: 1px solid #e3f2fd;
}

.spec-content p {
  margin: 8px 0;
  color: #424242;
}

.spec-content strong {
  color: #1976d2;
}

.spec-content ul {
  margin: 10px 0;
  padding-left: 20px;
}

.spec-content li {
  margin: 6px 0;
  color: #555;
  line-height: 1.4;
}

.tips-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 15px;
  margin-top: 20px;
}

.tip-card {
  background: white;
  padding: 18px;
  border-radius: 10px;
  box-shadow: 0 1px 8px rgba(0, 0, 0, 0.1);
  border-left: 4px solid #9c27b0;
}

.tip-card h6 {
  color: #7b1fa2;
  margin: 0 0 10px 0;
  font-size: 1em;
}

.tip-card p {
  margin: 0;
  color: #555;
  font-size: 0.9em;
  line-height: 1.4;
}

/* 詳細實作規格樣式 */
.detailed-specs {
  background: #f3e5f5;
  padding: 30px;
  border-radius: 15px;
  margin-top: 30px;
  border-left: 5px solid #9c27b0;
}

.detailed-specs h4 {
  color: #7b1fa2;
  margin-bottom: 20px;
  font-size: 1.4em;
  text-align: center;
}

.specs-intro {
  color: #424242;
  margin-bottom: 25px;
  font-size: 1.05em;
  line-height: 1.6;
  text-align: center;
}

/* 評估清單區塊樣式 */
.checklist-section {
  background: white;
  padding: 25px;
  border-radius: 12px;
  margin-bottom: 25px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.08);
  border: 1px solid #e0e0e0;
}

.checklist-section h5 {
  color: #1976d2;
  margin-bottom: 20px;
  font-size: 1.3em;
  border-bottom: 2px solid #e3f2fd;
  padding-bottom: 10px;
}

.checklist-group {
  margin-bottom: 25px;
  padding: 20px;
  background: #fafafa;
  border-radius: 10px;
  border-left: 4px solid #4caf50;
}

.checklist-group h6 {
  color: #2e7d32;
  margin: 0 0 15px 0;
  font-size: 1.1em;
  font-weight: 600;
}

.checklist {
  list-style: none;
  padding: 0;
  margin: 0;
}

.checklist li {
  padding: 8px 0;
  color: #424242;
  font-size: 0.95em;
  line-height: 1.5;
  position: relative;
  padding-left: 25px;
}

.checklist li:before {
  content: "□";
  position: absolute;
  left: 0;
  top: 8px;
  color: #4caf50;
  font-size: 1.1em;
  font-weight: bold;
}

.checklist li:hover {
  background: #f0f8ff;
  padding: 8px 10px;
  border-radius: 5px;
  margin: 0 -10px;
}

/* 組件清單樣式 */
.component-checklist {
  margin-bottom: 25px;
  padding: 20px;
  background: #fff8e1;
  border-radius: 10px;
  border-left: 4px solid #ff9800;
}

.component-checklist h6 {
  color: #e65100;
  margin: 0 0 15px 0;
  font-size: 1.1em;
  font-weight: 600;
}

/* 測試驗證區塊樣式 */
.testing-section {
  background: #e8f5e9;
  padding: 25px;
  border-radius: 12px;
  margin-top: 30px;
  border-left: 5px solid #4caf50;
}

.testing-section h5 {
  color: #2e7d32;
  margin-bottom: 20px;
  font-size: 1.3em;
  text-align: center;
}

.test-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
  margin-top: 20px;
}

.test-item {
  background: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  border: 1px solid #e0e0e0;
}

.test-item h6 {
  color: #1976d2;
  margin: 0 0 15px 0;
  font-size: 1.05em;
  font-weight: 600;
  border-bottom: 1px solid #e3f2fd;
  padding-bottom: 8px;
}

.test-item ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.test-item li {
  padding: 6px 0;
  color: #424242;
  font-size: 0.9em;
  line-height: 1.4;
  position: relative;
  padding-left: 25px;
}

.test-item li:before {
  content: "□";
  position: absolute;
  left: 0;
  top: 6px;
  color: #2196f3;
  font-size: 1em;
  font-weight: bold;
}

.test-item li:hover {
  background: #f0f8ff;
  padding: 6px 10px;
  border-radius: 4px;
  margin: 0 -10px;
}

@media (max-width: 768px) {
  .self-challenge-container {
    padding: 15px;
  }

  .header h2 {
    font-size: 2em;
  }

  .stats-grid {
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 15px;
  }

  .hints-grid {
    grid-template-columns: 1fr;
    gap: 15px;
  }

  .practice-details {
    padding: 20px;
  }

  .practice-grid {
    grid-template-columns: 1fr;
    gap: 15px;
  }

  .goals-grid {
    grid-template-columns: 1fr;
    gap: 12px;
  }

  .goal-item {
    padding: 12px;
  }

  .implementation-guide {
    padding: 20px;
  }

  .file-list {
    grid-template-columns: 1fr;
    gap: 8px;
  }

  .component-spec-grid {
    grid-template-columns: 1fr;
    gap: 15px;
  }

  .tips-grid {
    grid-template-columns: 1fr;
    gap: 12px;
  }

  /* 評估清單移動端響應式 */
  .detailed-specs {
    padding: 20px;
  }

  .checklist-section {
    padding: 20px;
  }

  .checklist-group {
    padding: 15px;
  }

  .component-checklist {
    padding: 15px;
  }

  .testing-section {
    padding: 20px;
  }

  .test-grid {
    grid-template-columns: 1fr;
    gap: 15px;
  }

  .test-item {
    padding: 15px;
  }
}
</style>
