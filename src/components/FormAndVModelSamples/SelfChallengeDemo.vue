<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - 表單輸入與 v-model</h2>
    <p class="route-info">📍 路徑：/FormAndVModelSamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>挑戰任務：</strong>建立一個完整的使用者註冊系統，實作各種表單控制元件和驗證
    </p>

    <div class="challenge-section">
      <h3>🎯 挑戰清單</h3>
      <div class="task-list">
        <div class="task-item">
          <input type="checkbox" id="task1">
          <label for="task1">1. 基本資料表單 - 使用者名稱、郵箱、密碼驗證</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task2">
          <label for="task2">2. 個人資訊 - 年齡、性別、城市、興趣選擇</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task3">
          <label for="task3">3. 帳號設定 - 條款同意、通知訂閱</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task4">
          <label for="task4">4. 表單操作 - 驗證、提交、重置、範例填入</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task5">
          <label for="task5">5. 即時預覽 - 資料展示與驗證狀態</label>
        </div>
      </div>
    </div>

    <div class="implementation-section">
      <h3>👨‍💻 實作練習詳情</h3>
      <p class="implementation-intro">
        📋 <strong>請完成使用者註冊系統的各項表單功能：</strong>
      </p>

      <div class="implementation-list">
        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">1.</span>
            <span class="function-name">表單驗證系統</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            實作完整的表單驗證機制，包含即時驗證和提交前驗證
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>使用者名稱：</strong>3-20字元，只能包含字母、數字、底線</li>
                <li><strong>電子郵件：</strong>符合標準電子郵件格式</li>
                <li><strong>密碼強度：</strong>至少8字元，包含大小寫字母和數字</li>
                <li><strong>確認密碼：</strong>必須與密碼完全相同</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作 validateUsername 方法檢查使用者名稱</li>
                <li>實作 validateEmail 方法檢查郵箱格式</li>
                <li>實作 validatePassword 方法檢查密碼強度</li>
                <li>實作 validateConfirmPassword 方法確認密碼</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">2.</span>
            <span class="function-name">多樣表單控制元件</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            運用各種表單控制元件，掌握 v-model 的不同用法
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>文字輸入：</strong>input text, email, password, number</li>
                <li><strong>選擇控制：</strong>radio button（性別）、select（城市）</li>
                <li><strong>多選控制：</strong>checkbox 陣列（興趣愛好）</li>
                <li><strong>文字區域：</strong>textarea（自我介紹）含字數統計</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>使用 v-model 綁定各種表單元件</li>
                <li>使用 v-model.number 處理數字輸入</li>
                <li>實作 checkbox 陣列的多選功能</li>
                <li>加入字數統計和輸入限制</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">3.</span>
            <span class="function-name">即時驗證與監聽</span>
            <span class="difficulty hard">困難</span>
          </div>
          <div class="function-description">
            使用 watch 監聽器實作即時表單驗證和錯誤提示
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>即時驗證：</strong>輸入時立即顯示驗證結果</li>
                <li><strong>錯誤提示：</strong>顯示具體的錯誤訊息</li>
                <li><strong>視覺回饋：</strong>錯誤欄位標示和樣式變化</li>
                <li><strong>驗證狀態：</strong>追蹤每個欄位的驗證狀態</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>使用 watch 監聽各個表單欄位變化</li>
                <li>在變化時自動執行對應的驗證方法</li>
                <li>更新錯誤狀態和錯誤訊息</li>
                <li>實作視覺化的驗證回饋</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">4.</span>
            <span class="function-name">表單操作與狀態管理</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            實作完整的表單操作功能，包含提交、重置和範例資料填入
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>表單提交：</strong>最終驗證後模擬 API 提交</li>
                <li><strong>表單重置：</strong>清空所有欄位和錯誤狀態</li>
                <li><strong>範例填入：</strong>填入測試資料方便開發</li>
                <li><strong>提交狀態：</strong>載入、成功、失敗狀態管理</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作 submitForm 方法處理表單提交</li>
                <li>實作 resetForm 方法重置表單狀態</li>
                <li>實作 fillSampleData 方法填入範例資料</li>
                <li>使用 isFormValid 計算屬性控制提交按鈕</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">5.</span>
            <span class="function-name">資料預覽與計算屬性</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            使用計算屬性提供即時的資料預覽和表單狀態顯示
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>資料預覽：</strong>格式化顯示當前表單資料</li>
                <li><strong>驗證狀態：</strong>視覺化顯示各欄位驗證結果</li>
                <li><strong>表單有效性：</strong>綜合判斷表單是否可提交</li>
                <li><strong>即時更新：</strong>資料變化時自動更新預覽</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作 formDataPreview 計算屬性格式化資料</li>
                <li>實作 isFormValid 計算屬性判斷表單有效性</li>
                <li>建立驗證狀態的視覺化顯示</li>
                <li>確保預覽資料的即時更新</li>
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
              <strong>基礎表單</strong>
              <p>建立表單資料結構和基本 v-model 綁定</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">2</div>
            <div class="step-content">
              <strong>驗證方法</strong>
              <p>實作各種表單驗證邏輯</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">3</div>
            <div class="step-content">
              <strong>即時監聽</strong>
              <p>加入 watch 監聽和即時驗證</p>
            </div>
          </div>
          <div class="flow-step">
            <div class="step-number">4</div>
            <div class="step-content">
              <strong>操作功能</strong>
              <p>完成提交、重置等操作功能</p>
            </div>
          </div>
        </div>
      </div>

      <div class="hint-section">
        <h4>💡 開發提示</h4>
        <details>
          <summary>點擊查看開發提示</summary>
          <div class="hints">
            <h5>v-model 使用技巧：</h5>
            <ul>
              <li><strong>基本用法：</strong>input、textarea、select 的雙向綁定</li>
              <li><strong>修飾符：</strong>.number（數字）、.trim（去空格）、.lazy（失焦更新）</li>
              <li><strong>checkbox：</strong>單個綁定 boolean，多個綁定陣列</li>
              <li><strong>radio：</strong>所有同組 radio 綁定同一個變數</li>
            </ul>

            <h5>常見問題解決：</h5>
            <ul>
              <li><strong>雙向綁定失效：</strong>檢查變數是否為響應式（ref）</li>
              <li><strong>驗證時機：</strong>使用 watch 進行即時驗證</li>
              <li><strong>陣列操作：</strong>checkbox 陣列要確保響應式更新</li>
              <li><strong>表單重置：</strong>重置時要清空錯誤狀態和驗證訊息</li>
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
  border-left: 5px solid #fd7e14;
}

.challenge-section h3 {
  color: #fd7e14;
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
  accent-color: #fd7e14;
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
  background: linear-gradient(135deg, #fd7e14 0%, #ff9800 100%);
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
