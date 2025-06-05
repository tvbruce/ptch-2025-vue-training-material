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
          <label for="task1">1. 創建 TaskItem 子組件，接收 props</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task2">
          <label for="task2">2. 實現父子組件通信（emit 事件）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task3">
          <label for="task3">3. 使用插槽（slot）自定義內容</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task4">
          <label for="task4">4. 實現組件間數據傳遞</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task5">
          <label for="task5">5. 創建可重用的 UI 組件</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task6">
          <label for="task6">6. 組件生命週期管理</label>
        </div>
      </div>
    </div>

    <div class="implementation-section">
      <h3>👨‍💻 實作練習詳情</h3>
      <p class="implementation-intro">
        📋 <strong>請完成以下組件化開發功能：</strong>
      </p>

      <div class="implementation-list">
        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">1.</span>
            <span class="function-name">TaskItem 組件</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            創建任務項目子組件
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>Props：</strong>task (Object), showPriority (Boolean)</li>
                <li><strong>事件：</strong>toggle-complete, delete-task</li>
                <li><strong>顯示：</strong>任務標題、完成狀態、優先級</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>創建獨立的 TaskItem.vue 組件</li>
                <li>定義 props 接收任務資料</li>
                <li>實現任務顯示和交互邏輯</li>
                <li>使用事件向父組件通信</li>
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
            創建任務表單組件
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>表單欄位：</strong>標題、描述、優先級、截止日期</li>
                <li><strong>驗證：</strong>標題不能為空</li>
                <li><strong>事件：</strong>add-task</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實現父子組件事件通信</li>
                <li>使用 emit 向父組件發送資料</li>
                <li>處理表單提交和驗證</li>
                <li>管理組件內部狀態</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">3.</span>
            <span class="function-name">Card 組件</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            創建可重用卡片組件
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>插槽：</strong>header, default, footer</li>
                <li><strong>Props：</strong>title, color, shadow</li>
                <li><strong>樣式：</strong>響應式設計</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>使用插槽自定義內容區域</li>
                <li>實現具名插槽和預設插槽</li>
                <li>提供靈活的內容結構</li>
                <li>支持動態內容插入</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">4.</span>
            <span class="function-name">組件數據流</span>
            <span class="difficulty hard">困難</span>
          </div>
          <div class="function-description">
            實現完整的組件數據傳遞
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>數據流向：</strong>父 → 子（props），子 → 父（events）</li>
                <li><strong>狀態管理：</strong>任務清單的增刪改查</li>
                <li><strong>響應式更新：</strong>即時同步所有組件狀態</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實現組件間數據雙向傳遞</li>
                <li>管理複雜的組件狀態</li>
                <li>處理多層級組件通信</li>
                <li>確保數據一致性</li>
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
            <h5>組件化開發要點：</h5>
            <ul>
              <li><strong>Props：</strong>父組件向子組件傳遞數據</li>
              <li><strong>Events：</strong>子組件向父組件發送事件</li>
              <li><strong>Slots：</strong>提供靈活的內容插入點</li>
              <li><strong>組件設計：</strong>單一職責、可重用、可組合</li>
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
