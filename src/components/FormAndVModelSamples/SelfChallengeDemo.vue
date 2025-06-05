<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - 表單輸入與 v-model</h2>
    <p class="route-info">📍 路徑：/FormAndVModelSamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>挑戰任務：</strong>建立一個用戶資料表單，練習 v-model 的各種用法
    </p>

    <div class="challenge-section">
      <h3>🎯 挑戰清單</h3>
      <div class="task-list">
        <div class="task-item">
          <input type="checkbox" id="task1">
          <label for="task1">1. 完成基本輸入欄位的 v-model 綁定</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task2">
          <label for="task2">2. 使用 v-model 修飾符（.trim、.number、.lazy）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task3">
          <label for="task3">3. 實作單選框和複選框綁定</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task4">
          <label for="task4">4. 完成下拉選單綁定（單選、多選）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task5">
          <label for="task5">5. 實作表單驗證邏輯</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task6">
          <label for="task6">6. 完成表單提交和重置功能</label>
        </div>
      </div>
    </div>

    <div class="implementation-section">
      <h3>👨‍💻 實作練習詳情</h3>
      <p class="implementation-intro">
        📋 <strong>請在 &lt;script setup&gt; 區域完成以下函數的實作：</strong>
      </p>

      <div class="implementation-list">
        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">1.</span>
            <span class="function-name">isFormValid (computed)</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            計算表單整體驗證狀態
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>姓名驗證：</strong>formData.name.trim().length >= 2</li>
                <li><strong>Email 驗證：</strong>使用正規表達式檢查格式</li>
                <li><strong>年齡驗證：</strong>18 <= formData.age <=100</li>
                <li><strong>性別驗證：</strong>formData.gender 不為空</li>
                <li><strong>興趣驗證：</strong>至少選擇一項興趣</li>
                <li><strong>返回值：</strong>所有條件都滿足時返回 true</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作基本輸入欄位的 v-model 綁定</li>
                <li>處理文字輸入、數字輸入、電子郵件輸入</li>
                <li>確保雙向資料綁定正常運作</li>
                <li>在預覽區域即時顯示輸入值</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">2.</span>
            <span class="function-name">validateEmail(email)</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            驗證 Email 格式是否正確
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>正規表達式：</strong>/^[^\s@]+@[^\s@]+\.[^\s@]+$/</li>
                <li><strong>參數：</strong>email (string) - 要驗證的 email 地址</li>
                <li><strong>返回值：</strong>boolean - 格式正確返回 true</li>
                <li><strong>空值處理：</strong>空字串返回 false</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>使用 v-model 修飾符優化輸入體驗</li>
                <li>實作 .trim 修飾符自動去除空白</li>
                <li>實作 .number 修飾符自動轉換數字</li>
                <li>理解 .lazy 修飾符的使用時機</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">3.</span>
            <span class="function-name">submitForm()</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            處理表單提交邏輯
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>驗證檢查：</strong>先檢查 isFormValid.value 是否為 true</li>
                <li><strong>提交狀態：</strong>設定 isSubmitting.value = true</li>
                <li><strong>模擬延遲：</strong>使用 setTimeout 模擬 2 秒提交過程</li>
                <li><strong>成功處理：</strong>設定 submitMessage.value = '表單提交成功！'</li>
                <li><strong>重置狀態：</strong>提交完成後重置 isSubmitting.value = false</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作性別單選框的 v-model 綁定</li>
                <li>實作興趣愛好複選框的 v-model 綁定</li>
                <li>理解單選框共用變數的概念</li>
                <li>理解複選框綁定到陣列的機制</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">4.</span>
            <span class="function-name">resetForm()</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            重置表單為初始狀態
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>基本資料：</strong>name = '', email = '', age = 18</li>
                <li><strong>選擇項目：</strong>gender = '', country = ''</li>
                <li><strong>多選項目：</strong>interests = [], languages = []</li>
                <li><strong>文字區域：</strong>bio = ''</li>
                <li><strong>狀態重置：</strong>submitMessage = '', isSubmitting = false</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>完成下拉選單的 v-model 綁定</li>
                <li>實作國家選擇的單選下拉選單</li>
                <li>實作語言多選的下拉選單</li>
                <li>處理 textarea 的 v-model 綁定</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">5.</span>
            <span class="function-name">getFormSummary() (computed)</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            生成表單資料摘要
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>格式化輸出：</strong>將表單資料整理成易讀格式</li>
                <li><strong>陣列處理：</strong>將 interests 和 languages 陣列轉為字串</li>
                <li><strong>空值處理：</strong>空值顯示為 '未填寫'</li>
                <li><strong>返回格式：</strong>物件包含所有格式化後的欄位</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作基本的表單驗證功能</li>
                <li>檢查必填欄位是否完整</li>
                <li>驗證電子郵件格式</li>
                <li>驗證年齡範圍的合理性</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">6.</span>
            <span class="function-name">handleAgeInput(event)</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            處理年齡輸入的特殊邏輯
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>數值轉換：</strong>將輸入值轉為數字</li>
                <li><strong>範圍限制：</strong>確保年齡在 1-120 之間</li>
                <li><strong>無效處理：</strong>非數字輸入時保持原值</li>
                <li><strong>即時更新：</strong>更新 formData.age</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>完成表單提交和重置功能</li>
                <li>實作表單驗證邏輯</li>
                <li>處理提交成功和失敗狀態</li>
                <li>實作表單重置為初始狀態</li>
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
            <pre><code>// 基本 v-model 綁定
&lt;input v-model="inputValue" type="text"&gt;
&lt;textarea v-model="textareaValue"&gt;&lt;/textarea&gt;

// v-model 修飾符
&lt;input v-model.trim="username"&gt;      // 去除空白
&lt;input v-model.number="age"&gt;        // 轉為數字
&lt;input v-model.lazy="description"&gt;  // 失焦時更新

// 單選框綁定
&lt;input type="radio" v-model="gender" value="male"&gt;
&lt;input type="radio" v-model="gender" value="female"&gt;

// 複選框綁定（多選）
&lt;input type="checkbox" v-model="hobbies" value="reading"&gt;
&lt;input type="checkbox" v-model="hobbies" value="music"&gt;

// 下拉選單
&lt;select v-model="country"&gt;
  &lt;option value="taiwan"&gt;台灣&lt;/option&gt;
  &lt;option value="china"&gt;中國&lt;/option&gt;
&lt;/select&gt;

// 多選下拉選單
&lt;select v-model="languages" multiple&gt;
  &lt;option value="zh"&gt;中文&lt;/option&gt;
  &lt;option value="en"&gt;英文&lt;/option&gt;
&lt;/select&gt;</code></pre>

            <h5>重要概念：</h5>
            <ul>
              <li><strong>v-model 修飾符：</strong>.trim 去除空白、.number 轉數字、.lazy 失焦時更新</li>
              <li><strong>表單驗證：</strong>使用 computed 屬性實現即時驗證</li>
              <li><strong>陣列綁定：</strong>checkbox 和 select multiple 會自動處理陣列</li>
              <li><strong>非同步處理：</strong>使用 Promise 或 setTimeout 模擬 API 呼叫</li>
              <li><strong>狀態管理：</strong>合理使用 ref 和 reactive 管理表單狀態</li>
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
