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

    <!-- 學員練習任務區塊 -->
    <div class="practice-tasks-section">
      <h3>📚 學員練習任務詳情</h3>
      <div class="practice-tasks">

        <div class="practice-task">
          <h4>任務 1：基本輸入欄位的 v-model 綁定</h4>
          <div class="task-details">
            <p><strong>目標：</strong>為文字輸入框、數字輸入框、電子郵件輸入框綁定 v-model</p>
            <p><strong>需要實作：</strong></p>
            <ul>
              <li>為 <code>username</code> 輸入框添加 <code>v-model="formData.username"</code></li>
              <li>為 <code>email</code> 輸入框添加 <code>v-model="formData.email"</code></li>
              <li>為 <code>age</code> 輸入框添加 <code>v-model="formData.age"</code></li>
            </ul>
            <p><strong>驗證方式：</strong>輸入內容後，下方預覽區應該即時顯示輸入的值</p>
          </div>
        </div>

        <div class="practice-task">
          <h4>任務 2：使用 v-model 修飾符</h4>
          <div class="task-details">
            <p><strong>目標：</strong>學習使用 .trim 和 .number 修飾符</p>
            <p><strong>需要實作：</strong></p>
            <ul>
              <li>為 <code>username</code> 添加 <code>.trim</code> 修飾符，自動去除前後空格</li>
              <li>為 <code>age</code> 添加 <code>.number</code> 修飾符，自動轉換為數字類型</li>
            </ul>
            <p><strong>測試方式：</strong>在用戶名前後輸入空格，應該自動去除；年齡應該自動轉為數字</p>
          </div>
        </div>

        <div class="practice-task">
          <h4>任務 3：單選框和複選框綁定</h4>
          <div class="task-details">
            <p><strong>目標：</strong>實作性別單選和興趣愛好多選</p>
            <p><strong>需要實作：</strong></p>
            <ul>
              <li>為所有性別單選框添加 <code>v-model="formData.gender"</code></li>
              <li>為所有興趣愛好複選框添加 <code>v-model="formData.hobbies"</code></li>
            </ul>
            <p><strong>邏輯說明：</strong>單選框共用一個變數，複選框綁定到陣列</p>
          </div>
        </div>

        <div class="practice-task">
          <h4>任務 4：下拉選單綁定</h4>
          <div class="task-details">
            <p><strong>目標：</strong>完成國家選擇和語言多選</p>
            <p><strong>需要實作：</strong></p>
            <ul>
              <li>為國家選擇框添加 <code>v-model="formData.country"</code></li>
              <li>為語言多選框添加 <code>v-model="formData.languages"</code></li>
              <li>為個人簡介文字域添加 <code>v-model="formData.bio"</code></li>
            </ul>
            <p><strong>注意：</strong>多選下拉選單會自動綁定到陣列</p>
          </div>
        </div>

        <div class="practice-task">
          <h4>任務 5：表單驗證邏輯</h4>
          <div class="task-details">
            <p><strong>目標：</strong>實作基本的表單驗證功能</p>
            <p><strong>需要實作：</strong></p>
            <ul>
              <li>完成 <code>validateForm()</code> 函數</li>
              <li>檢查用戶名不能為空（去除空格後）</li>
              <li>檢查電子郵件格式是否正確</li>
              <li>檢查年齡是否在 1-120 之間</li>
            </ul>
            <p><strong>邏輯說明：</strong>驗證失敗時，將錯誤訊息存入 <code>errors</code> 物件中</p>
            <div class="code-example">
              <pre><code>// 範例邏輯
if (!formData.value.username.trim()) {
  errors.value.username = '用戶名不能為空'
}</code></pre>
            </div>
          </div>
        </div>

        <div class="practice-task">
          <h4>任務 6：表單提交和重置功能</h4>
          <div class="task-details">
            <p><strong>目標：</strong>完成表單的提交和重置邏輯</p>
            <p><strong>需要實作：</strong></p>
            <ul>
              <li>完成 <code>submitForm()</code> 函數：先驗證表單，通過後顯示成功訊息</li>
              <li>完成 <code>resetForm()</code> 函數：重置所有表單資料為初始值</li>
              <li>完成 <code>isFormValid</code> 計算屬性：檢查表單是否有效</li>
            </ul>
            <p><strong>邏輯說明：</strong></p>
            <ul>
              <li>提交時先清空錯誤訊息，再進行驗證</li>
              <li>重置時要將所有欄位恢復初始狀態</li>
              <li>表單有效性基於是否有錯誤訊息來判斷</li>
            </ul>
          </div>
        </div>
      </div>
    </div>

    <div class="demo-section">
      <h3>📝 用戶資料表單</h3>
      <form @submit.prevent="submitForm" class="registration-form">

        <!-- 基本資訊 -->
        <div class="form-section">
          <h4>基本資訊</h4>

          <div class="form-group">
            <label for="username">用戶名：</label>
            <!-- 任務 1 & 2: 在這裡添加 v-model.trim -->
            <input id="username" type="text" placeholder="請輸入用戶名" class="form-input"
              :class="{ 'error': errors.username }">
            <span v-if="errors.username" class="error-msg">{{ errors.username }}</span>
          </div>

          <div class="form-group">
            <label for="email">電子郵件：</label>
            <!-- 任務 1: 在這裡添加 v-model -->
            <input id="email" type="email" placeholder="請輸入電子郵件" class="form-input" :class="{ 'error': errors.email }">
            <span v-if="errors.email" class="error-msg">{{ errors.email }}</span>
          </div>

          <div class="form-group">
            <label for="age">年齡：</label>
            <!-- 任務 1 & 2: 在這裡添加 v-model.number -->
            <input id="age" type="number" placeholder="請輸入年齡" class="form-input" min="1" max="120"
              :class="{ 'error': errors.age }">
            <span v-if="errors.age" class="error-msg">{{ errors.age }}</span>
          </div>
        </div>

        <!-- 個人偏好 -->
        <div class="form-section">
          <h4>個人偏好</h4>

          <div class="form-group">
            <label>性別：</label>
            <!-- 任務 3: 為每個單選框添加 v-model="formData.gender" -->
            <div class="radio-group">
              <label class="radio-label">
                <input type="radio" value="male"> 男性
              </label>
              <label class="radio-label">
                <input type="radio" value="female"> 女性
              </label>
              <label class="radio-label">
                <input type="radio" value="other"> 其他
              </label>
            </div>
          </div>

          <div class="form-group">
            <label>興趣愛好：</label>
            <!-- 任務 3: 為每個複選框添加 v-model="formData.hobbies" -->
            <div class="checkbox-group">
              <label class="checkbox-label">
                <input type="checkbox" value="reading"> 閱讀
              </label>
              <label class="checkbox-label">
                <input type="checkbox" value="music"> 音樂
              </label>
              <label class="checkbox-label">
                <input type="checkbox" value="sports"> 運動
              </label>
              <label class="checkbox-label">
                <input type="checkbox" value="travel"> 旅行
              </label>
            </div>
          </div>

          <div class="form-group">
            <label for="country">居住國家：</label>
            <!-- 任務 4: 在這裡添加 v-model -->
            <select id="country" class="form-select">
              <option value="">請選擇國家</option>
              <option value="taiwan">台灣</option>
              <option value="china">中國</option>
              <option value="japan">日本</option>
              <option value="korea">韓國</option>
              <option value="usa">美國</option>
            </select>
          </div>

          <div class="form-group">
            <label for="languages">會說的語言：</label>
            <!-- 任務 4: 在這裡添加 v-model -->
            <select id="languages" multiple class="form-select multi-select">
              <option value="chinese">中文</option>
              <option value="english">英文</option>
              <option value="japanese">日文</option>
              <option value="korean">韓文</option>
            </select>
            <small class="help-text">按住 Ctrl (或 Cmd) 可以多選</small>
          </div>

          <div class="form-group">
            <label for="bio">個人簡介：</label>
            <!-- 任務 4: 在這裡添加 v-model -->
            <textarea id="bio" placeholder="請簡單介紹自己..." class="form-textarea" rows="3">
            </textarea>
          </div>
        </div>

        <div class="form-actions">
          <button type="button" @click="resetForm" class="btn btn-secondary">重置表單</button>
          <button type="submit" class="btn btn-primary" :disabled="!isFormValid">提交</button>
        </div>
      </form>
    </div>

    <div class="demo-section">
      <h3>📋 表單預覽</h3>
      <div class="form-preview">
        <div class="preview-section">
          <h4>基本資訊</h4>
          <p><strong>用戶名：</strong>{{ formData.username || '未填寫' }}</p>
          <p><strong>電子郵件：</strong>{{ formData.email || '未填寫' }}</p>
          <p><strong>年齡：</strong>{{ formData.age || '未填寫' }}</p>
        </div>

        <div class="preview-section">
          <h4>個人偏好</h4>
          <p><strong>性別：</strong>{{ formData.gender || '未選擇' }}</p>
          <p><strong>興趣愛好：</strong>{{ formData.hobbies.length ? formData.hobbies.join(', ') : '未選擇' }}</p>
          <p><strong>居住國家：</strong>{{ formData.country || '未選擇' }}</p>
          <p><strong>會說的語言：</strong>{{ formData.languages.length ? formData.languages.join(', ') : '未選擇' }}</p>
          <p><strong>個人簡介：</strong>{{ formData.bio || '未填寫' }}</p>
        </div>
      </div>
    </div>

    <div class="hint-section">
      <h4>💡 快速參考</h4>
      <details>
        <summary>點擊查看 v-model 語法參考</summary>
        <div class="reference-content">
          <div class="ref-item">
            <h5>基本綁定</h5>
            <pre><code>&lt;input v-model="變數名" type="text"&gt;</code></pre>
          </div>
          <div class="ref-item">
            <h5>修飾符</h5>
            <pre><code>&lt;input v-model.trim="變數名"&gt;     // 去除空格
&lt;input v-model.number="變數名"&gt;   // 轉為數字</code></pre>
          </div>
          <div class="ref-item">
            <h5>單選框</h5>
            <pre><code>&lt;input v-model="gender" type="radio" value="male"&gt;
&lt;input v-model="gender" type="radio" value="female"&gt;</code></pre>
          </div>
          <div class="ref-item">
            <h5>複選框（多選）</h5>
            <pre><code>&lt;input v-model="hobbies" type="checkbox" value="reading"&gt;
&lt;input v-model="hobbies" type="checkbox" value="music"&gt;</code></pre>
          </div>
        </div>
      </details>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 表單資料
const formData = ref({
  username: '',
  email: '',
  age: null,
  gender: '',
  hobbies: [],
  country: '',
  languages: [],
  bio: ''
})

// 錯誤訊息
const errors = ref({})

// 任務 5: 完成表單驗證邏輯
const validateForm = () => {
  // 先清空之前的錯誤訊息
  errors.value = {}

  // 在這裡添加驗證邏輯
  // 提示：檢查用戶名、電子郵件、年齡

  // 返回是否驗證通過
  return Object.keys(errors.value).length === 0
}

// 任務 6: 完成表單有效性檢查
const isFormValid = computed(() => {
  // 在這裡添加邏輯，檢查表單是否可以提交
  // 提示：可以基於是否有必填欄位來判斷
  return false
})

// 任務 6: 完成表單提交邏輯
const submitForm = () => {
  // 在這裡添加提交邏輯
  // 1. 先進行表單驗證
  // 2. 如果驗證通過，顯示成功訊息
  console.log('表單提交功能待實作')
}

// 任務 6: 完成表單重置邏輯
const resetForm = () => {
  // 在這裡添加重置邏輯
  // 提示：將所有 formData 的值重置為初始狀態
  console.log('表單重置功能待實作')
}
</script>

<style scoped>
/* 使用統一的自我試煉樣式 */
@import '@/assets/self-challenge.css';

.self-challenge {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}



.challenge-section {
  background: #fff3e0;
  padding: 1.5rem;
  border-radius: 8px;
  margin: 2rem 0;
}

.task-list {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.task-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.5rem;
  background: white;
  border-radius: 4px;
}

.task-item.completed {
  background: #e8f5e8;
}

.task-item input[type="checkbox"] {
  width: 18px;
  height: 18px;
}

/* 學員練習任務樣式 */
.practice-tasks-section {
  background: #f0f8ff;
  padding: 2rem;
  border-radius: 8px;
  margin: 2rem 0;
  border: 2px solid #1976d2;
}

.practice-tasks {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.practice-task {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  border-left: 4px solid #1976d2;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.practice-task h4 {
  margin: 0 0 1rem 0;
  color: #1976d2;
  font-size: 1.1rem;
}

.task-details p {
  margin: 0.5rem 0;
}

.task-details ul {
  margin: 0.5rem 0;
  padding-left: 1.5rem;
}

.task-details li {
  margin: 0.3rem 0;
}

.code-example {
  margin: 1rem 0;
}

.code-example pre {
  background: #2d3748;
  color: #e2e8f0;
  padding: 1rem;
  border-radius: 4px;
  overflow-x: auto;
  font-size: 0.9rem;
}

.demo-section {
  margin: 2rem 0;
  padding: 1.5rem;
  border: 1px solid #ddd;
  border-radius: 8px;
  background: #fafafa;
}

.registration-form {
  max-width: 800px;
}

.form-section {
  margin-bottom: 2rem;
  padding: 1.5rem;
  background: white;
  border-radius: 8px;
  border: 1px solid #e0e0e0;
}

.form-section h4 {
  margin: 0 0 1rem 0;
  padding-bottom: 0.5rem;
  border-bottom: 1px solid #e0e0e0;
  color: #1976d2;
}

.form-group {
  margin-bottom: 1rem;
}

.form-group label {
  display: block;
  font-weight: bold;
  margin-bottom: 0.5rem;
  color: #333;
}

.form-input,
.form-select,
.form-textarea {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 1rem;
  transition: border-color 0.2s;
}

.form-input:focus,
.form-select:focus,
.form-textarea:focus {
  outline: none;
  border-color: #1976d2;
  box-shadow: 0 0 0 2px rgba(25, 118, 210, 0.1);
}

.form-input.error,
.form-select.error,
.form-textarea.error {
  border-color: #f44336;
}

.multi-select {
  height: 100px;
}

.radio-group,
.checkbox-group {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  margin-top: 0.5rem;
}

.radio-label,
.checkbox-label {
  display: flex !important;
  align-items: center;
  gap: 0.5rem;
  font-weight: normal !important;
  margin-bottom: 0 !important;
  cursor: pointer;
}

.radio-label input,
.checkbox-label input {
  width: auto !important;
  margin: 0;
}

.error-msg {
  color: #f44336;
  font-size: 0.875rem;
  margin-top: 0.25rem;
  display: block;
}

.help-text {
  color: #666;
  font-size: 0.875rem;
  margin-top: 0.25rem;
  display: block;
}

.form-actions {
  display: flex;
  gap: 1rem;
  justify-content: flex-end;
  margin-top: 2rem;
  padding-top: 1rem;
  border-top: 1px solid #e0e0e0;
}

.form-preview {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  border: 1px solid #e0e0e0;
}

.preview-section {
  margin-bottom: 1.5rem;
  padding-bottom: 1rem;
  border-bottom: 1px solid #f0f0f0;
}

.preview-section:last-child {
  border-bottom: none;
  margin-bottom: 0;
}

.preview-section h4 {
  margin: 0 0 0.5rem 0;
  color: #1976d2;
}

.preview-section p {
  margin: 0.25rem 0;
  color: #333;
}

.btn {
  padding: 0.75rem 1.5rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
  transition: background-color 0.2s;
}

.btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.btn-primary {
  background: #1976d2;
  color: white;
}

.btn-secondary {
  background: #757575;
  color: white;
}

.btn:hover:not(:disabled) {
  opacity: 0.9;
}

.hint-section {
  background: #e8f5e8;
  padding: 1.5rem;
  border-radius: 8px;
  margin: 2rem 0;
}

details {
  margin-top: 1rem;
}

summary {
  cursor: pointer;
  font-weight: bold;
  padding: 0.5rem;
  background: #c8e6c9;
  border-radius: 4px;
}

.reference-content {
  margin-top: 1rem;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1rem;
}

.ref-item {
  background: white;
  padding: 1rem;
  border-radius: 4px;
  border: 1px solid #e0e0e0;
}

.ref-item h5 {
  margin: 0 0 0.5rem 0;
  color: #1976d2;
}

.ref-item pre {
  background: #2d3748;
  color: #e2e8f0;
  padding: 0.75rem;
  border-radius: 4px;
  overflow-x: auto;
  font-size: 0.85rem;
  margin: 0;
}
</style>
