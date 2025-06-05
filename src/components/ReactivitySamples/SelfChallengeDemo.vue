<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - Reactivity 響應式</h2>
    <p class="route-info">📍 路徑：/ReactivitySamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>學習目標：</strong>掌握 Vue 3 響應式系統的基本概念，理解 ref 和 reactive 的使用時機
    </p>

    <div class="challenge-section">
      <h3>🎯 挑戰清單</h3>
      <div class="task-list">
        <div class="task-item">
          <input type="checkbox" id="task1">
          <label for="task1">1. 實作基本的 ref 響應式變數</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task2">
          <label for="task2">2. 實作 reactive 物件響應式</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task3">
          <label for="task3">3. 理解深層響應式的運作</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task4">
          <label for="task4">4. 實作 computed 響應式計算</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task5">
          <label for="task5">5. 處理響應式陣列操作</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task6">
          <label for="task6">6. 建立完整的用戶資料管理系統</label>
        </div>
      </div>
    </div>

    <div class="implementation-section">
      <h3>👨‍💻 實作練習詳情</h3>
      <p class="implementation-intro">
        📋 <strong>請在 &lt;script setup&gt; 區域完成以下響應式變數和函數的實作：</strong>
      </p>

      <div class="implementation-list">
        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">1.</span>
            <span class="function-name">基本 ref 變數</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            使用 ref 創建基本響應式變數
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>name (ref)：</strong>字串類型，預設值為 '小明'</li>
                <li><strong>age (ref)：</strong>數字類型，預設值為 25</li>
                <li><strong>isStudent (ref)：</strong>布林類型，預設值為 true</li>
                <li><strong>hobbies (ref)：</strong>陣列類型，預設值為 ['讀書', '運動']</li>
                <li><strong>訪問：</strong>在 template 中直接使用，在 script 中使用 .value</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>使用 ref() 創建響應式變數</li>
                <li>在 template 中顯示資料</li>
                <li>實作資料修改功能</li>
                <li>觀察響應式更新效果</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">2.</span>
            <span class="function-name">reactive 物件</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            使用 reactive 創建複雜物件響應式
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>userProfile (reactive)：</strong>包含 name, email, avatar 屬性</li>
                <li><strong>settings (reactive)：</strong>包含 theme, language, notifications 設定</li>
                <li><strong>stats (reactive)：</strong>包含 loginCount, lastLoginTime, score 統計</li>
                <li><strong>嵌套物件：</strong>支援深層響應式更新</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>使用 reactive() 創建物件響應式</li>
                <li>處理嵌套物件屬性</li>
                <li>實作物件屬性更新</li>
                <li>理解深層響應式特性</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">3.</span>
            <span class="function-name">updateUserName(newName)</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            更新用戶名稱（同時更新 ref 和 reactive）
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>參數：</strong>newName (string) - 新的用戶名稱</li>
                <li><strong>驗證：</strong>檢查名稱不為空且長度在 2-20 字元</li>
                <li><strong>更新：</strong>同時更新 name.value 和 userProfile.name</li>
                <li><strong>時間戳：</strong>更新 stats.lastLoginTime 為當前時間</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">4.</span>
            <span class="function-name">userDisplayName (computed)</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            計算用戶顯示名稱
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>邏輯：</strong>結合 name.value 和 age.value</li>
                <li><strong>格式：</strong>'{name} ({age}歲)' 如果是學生則加上 '(學生)'</li>
                <li><strong>示例：</strong>'小明 (25歲) (學生)' 或 '小華 (30歲)'</li>
                <li><strong>響應性：</strong>當 name、age 或 isStudent 改變時自動更新</li>
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
            <pre><code>// 基本響應式變數
import { ref, reactive, computed } from 'vue'

// ref 適用於基本類型
const name = ref('小明')
const age = ref(25)

// reactive 適用於物件和陣列
const userProfile = reactive({
  name: '小明',
  email: 'example@email.com'
})

// 計算屬性
const displayName = computed(() => {
  return `${name.value} (${age.value}歲)`
})</code></pre>

            <h5>重要概念：</h5>
            <ul>
              <li><strong>ref vs reactive：</strong>ref 適用於基本類型，reactive 適用於物件和陣列</li>
              <li><strong>.value 訪問：</strong>ref 在 script 中需要 .value，template 中自動解包</li>
              <li><strong>響應性保持：</strong>避免解構 reactive 物件，會失去響應性</li>
              <li><strong>陣列方法：</strong>push(), splice(), pop() 等方法會觸發響應式更新</li>
              <li><strong>computed 特性：</strong>基於依賴的響應式資料，當依賴改變時自動重新計算</li>
            </ul>
          </div>
        </details>
      </div>
    </div>

    <!-- 學員練習區塊 -->
    <div class="demo-section">
      <h3>🔧 學員練習區域</h3>
      <p class="hint">
        💡 <strong>提示：</strong>請根據上方的實作練習詳情完成以下功能實作
      </p>

      <!-- 任務一：基本 ref 響應式 -->
      <div class="task-section">
        <h4>任務一：基本 ref 響應式實作</h4>
        <div class="practice-area">
          <div class="user-info">
            <h5>用戶基本資訊</h5>
            <!-- TODO: 學員需要在這裡實作響應式資料顯示 -->
            <p>姓名：[請實作 name 顯示]</p>
            <p>年齡：[請實作 age 顯示]</p>
            <p>身份：[請實作 isStudent 條件顯示]</p>
            <p>興趣：[請實作 hobbies 陣列顯示]</p>
          </div>

          <div class="controls">
            <input placeholder="修改姓名" class="input-field">
            <input placeholder="修改年齡" type="number" class="input-field">
            <label class="checkbox-label">
              <input type="checkbox">
              是學生
            </label>
          </div>
        </div>
      </div>

      <!-- 任務二：reactive 物件響應式 -->
      <div class="task-section">
        <h4>任務二：reactive 物件響應式實作</h4>
        <div class="practice-area">
          <div class="profile-section">
            <h5>用戶檔案（reactive）</h5>
            <!-- TODO: 學員需要在這裡實作 reactive 物件顯示 -->
            <p>檔案名稱：[請實作 userProfile.name]</p>
            <p>電子郵件：[請實作 userProfile.email]</p>
            <p>頭像：[請實作 userProfile.avatar]</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted } from 'vue'

// TODO: 學員需要在這裡實作響應式變數和函數
// 需要導入：ref, reactive, computed

// 基本 ref 響應式變數
// const name = ref('小明')
// const age = ref(25)
// const isStudent = ref(true)
// const hobbies = ref(['讀書', '運動'])

// reactive 物件
// const userProfile = reactive({
//   name: '小明',
//   email: 'xiaoming@example.com',
//   avatar: 'https://via.placeholder.com/100'
// })

// 計算屬性
// const userDisplayName = computed(() => {
//   // TODO: 實作用戶顯示名稱計算邏輯
// })

// 函數實作
// const updateUserName = (newName) => {
//   // TODO: 實作用戶名稱更新邏輯
// }

onMounted(() => {
  console.log('響應式組件已載入')
})
</script>

<style scoped>
@import '@/assets/main.css';

.user-info,
.profile-section {
  background: #f8f9fa;
  padding: 1rem;
  border-radius: 8px;
  margin-bottom: 1rem;
}

.controls {
  display: flex;
  gap: 0.5rem;
  align-items: center;
  margin-top: 1rem;
  flex-wrap: wrap;
}

.input-field {
  padding: 0.5rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  flex: 1;
  min-width: 150px;
}

.checkbox-label {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  cursor: pointer;
}
</style>
