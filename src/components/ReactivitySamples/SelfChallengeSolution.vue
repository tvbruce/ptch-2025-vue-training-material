<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉解答 - Reactivity 響應式</h2>
    <p class="route-info">📍 路徑：/ReactivitySamples/SelfChallengeSolution.vue</p>
    <p class="description">
      ✅ <strong>完整解答：</strong>Vue 3 響應式系統的完整實作範例
    </p>

    <div class="solution-overview">
      <h3>📋 解答概覽</h3>
      <div class="feature-list">
        <div class="feature-item completed">
          <span class="icon">✅</span>
          <span>基本 ref 響應式變數實作</span>
        </div>
        <div class="feature-item completed">
          <span class="icon">✅</span>
          <span>reactive 物件響應式實作</span>
        </div>
        <div class="feature-item completed">
          <span class="icon">✅</span>
          <span>深層響應式處理</span>
        </div>
        <div class="feature-item completed">
          <span class="icon">✅</span>
          <span>computed 響應式計算</span>
        </div>
        <div class="feature-item completed">
          <span class="icon">✅</span>
          <span>響應式陣列操作</span>
        </div>
        <div class="feature-item completed">
          <span class="icon">✅</span>
          <span>完整用戶資料管理系統</span>
        </div>
      </div>
    </div>

    <!-- 任務一：基本 ref 響應式 -->
    <div class="task-section">
      <h4>✅ 任務一：基本 ref 響應式實作</h4>
      <div class="practice-area">
        <div class="user-info">
          <h5>用戶基本資訊</h5>
          <p>姓名：{{ name }}</p>
          <p>年齡：{{ age }}</p>
          <p>身份：{{ isStudent ? '學生' : '非學生' }}</p>
          <p>興趣：{{ hobbies.join(', ') }}</p>
          <p>計算顯示名稱：{{ userDisplayName }}</p>
        </div>

        <div class="controls">
          <input v-model="nameInput" placeholder="修改姓名" class="input-field" @keyup.enter="updateUserName(nameInput)">
          <button @click="updateUserName(nameInput)" class="btn-primary">更新姓名</button>
          <input v-model.number="age" placeholder="修改年齡" type="number" class="input-field">
          <label class="checkbox-label">
            <input type="checkbox" v-model="isStudent">
            是學生
          </label>
        </div>

        <div class="hobby-section">
          <h6>興趣管理</h6>
          <div class="hobby-controls">
            <input v-model="newHobby" placeholder="新增興趣" class="input-field" @keyup.enter="addHobby">
            <button @click="addHobby" class="btn-secondary">新增</button>
          </div>
          <div class="hobby-list">
            <span v-for="(hobby, index) in hobbies" :key="index" class="hobby-tag" @click="removeHobby(index)">
              {{ hobby }} ✕
            </span>
          </div>
        </div>
      </div>
    </div>

    <!-- 任務二：reactive 物件響應式 -->
    <div class="task-section">
      <h4>✅ 任務二：reactive 物件響應式實作</h4>
      <div class="practice-area">
        <div class="profile-section">
          <h5>用戶檔案（reactive）</h5>
          <p>檔案名稱：{{ userProfile.name }}</p>
          <p>電子郵件：{{ userProfile.email }}</p>
          <p>頭像：<img :src="userProfile.avatar" :alt="userProfile.name" class="avatar"></p>
          <p>登入次數：{{ stats.loginCount }}</p>
          <p>最後登入：{{ stats.lastLoginTime }}</p>
          <p>分數：{{ stats.score }}</p>
        </div>

        <div class="profile-controls">
          <input v-model="userProfile.email" placeholder="修改電子郵件" class="input-field">
          <button @click="updateAvatar" class="btn-secondary">更換頭像</button>
          <button @click="simulateLogin" class="btn-primary">模擬登入</button>
        </div>

        <div class="settings-section">
          <h6>用戶設定</h6>
          <div class="setting-item">
            <label>主題：</label>
            <select v-model="settings.theme" class="select-field">
              <option value="light">淺色</option>
              <option value="dark">深色</option>
              <option value="auto">自動</option>
            </select>
          </div>
          <div class="setting-item">
            <label>語言：</label>
            <select v-model="settings.language" class="select-field">
              <option value="zh-TW">繁體中文</option>
              <option value="zh-CN">簡體中文</option>
              <option value="en">English</option>
            </select>
          </div>
          <div class="setting-item">
            <label class="checkbox-label">
              <input type="checkbox" v-model="settings.notifications">
              啟用通知
            </label>
          </div>
        </div>
      </div>
    </div>

    <!-- 任務三：深層響應式和計算屬性展示 -->
    <div class="task-section">
      <h4>✅ 任務三：深層響應式和計算屬性</h4>
      <div class="practice-area">
        <div class="computed-demo">
          <h5>計算屬性示範</h5>
          <div class="computed-display">
            <p><strong>完整用戶資訊：</strong></p>
            <div class="user-card">
              <h6>{{ userDisplayName }}</h6>
              <p>📧 {{ userProfile.email }}</p>
              <p>🎨 主題：{{ settings.theme }}</p>
              <p>🌍 語言：{{ settings.language }}</p>
              <p>🔔 通知：{{ settings.notifications ? '開啟' : '關閉' }}</p>
              <p>📊 統計：登入 {{ stats.loginCount }} 次，分數 {{ stats.score }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- 實作說明 -->
    <div class="implementation-notes">
      <h3>💡 實作重點說明</h3>
      <div class="notes-grid">
        <div class="note-card">
          <h4>ref 響應式</h4>
          <ul>
            <li>適用於基本類型：string, number, boolean</li>
            <li>在 script 中需要使用 .value 訪問</li>
            <li>在 template 中自動解包</li>
            <li>可以綁定到表單元素進行雙向綁定</li>
          </ul>
        </div>
        <div class="note-card">
          <h4>reactive 響應式</h4>
          <ul>
            <li>適用於物件和陣列</li>
            <li>提供深層響應式</li>
            <li>不需要 .value 語法</li>
            <li>解構會失去響應性，需使用 toRefs</li>
          </ul>
        </div>
        <div class="note-card">
          <h4>computed 計算屬性</h4>
          <ul>
            <li>基於響應式依賴進行緩存</li>
            <li>只有依賴改變時才重新計算</li>
            <li>適合用於復雜的資料處理</li>
            <li>可以是只讀或可寫的</li>
          </ul>
        </div>
        <div class="note-card">
          <h4>最佳實踐</h4>
          <ul>
            <li>根據資料類型選擇 ref 或 reactive</li>
            <li>避免過度嵌套響應式物件</li>
            <li>使用 computed 而非 methods 處理衍生資料</li>
            <li>注意響應式資料的生命週期</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, computed, onMounted } from 'vue'

// ===== 任務一：基本 ref 響應式變數 =====
const name = ref('小明')
const age = ref(25)
const isStudent = ref(true)
const hobbies = ref(['讀書', '運動'])

// 輔助變數
const nameInput = ref('')
const newHobby = ref('')

// ===== 任務二：reactive 物件 =====
const userProfile = reactive({
  name: '小明',
  email: 'xiaoming@example.com',
  avatar: 'https://via.placeholder.com/100/4CAF50/ffffff?text=XM'
})

const settings = reactive({
  theme: 'light',
  language: 'zh-TW',
  notifications: true
})

const stats = reactive({
  loginCount: 1,
  lastLoginTime: new Date().toLocaleString(),
  score: 100
})

// ===== 任務三：計算屬性 =====
const userDisplayName = computed(() => {
  const studentText = isStudent.value ? ' (學生)' : ''
  return `${name.value} (${age.value}歲)${studentText}`
})

// ===== 任務四：函數實作 =====
const updateUserName = (newName) => {
  if (!newName || newName.trim().length < 2 || newName.trim().length > 20) {
    alert('姓名長度必須在 2-20 字元之間')
    return
  }

  // 同時更新 ref 和 reactive
  name.value = newName.trim()
  userProfile.name = newName.trim()

  // 更新時間戳
  stats.lastLoginTime = new Date().toLocaleString()

  // 清空輸入框
  nameInput.value = ''
}

// ===== 輔助函數 =====
const addHobby = () => {
  if (newHobby.value.trim() && !hobbies.value.includes(newHobby.value.trim())) {
    hobbies.value.push(newHobby.value.trim())
    newHobby.value = ''
  }
}

const removeHobby = (index) => {
  hobbies.value.splice(index, 1)
}

const updateAvatar = () => {
  const colors = ['4CAF50', 'FF9800', '2196F3', 'E91E63', '9C27B0']
  const randomColor = colors[Math.floor(Math.random() * colors.length)]
  const initials = userProfile.name.substring(0, 2).toUpperCase()
  userProfile.avatar = `https://via.placeholder.com/100/${randomColor}/ffffff?text=${initials}`
}

const simulateLogin = () => {
  stats.loginCount++
  stats.lastLoginTime = new Date().toLocaleString()
  stats.score += 10
}

onMounted(() => {
  console.log('響應式解答組件已載入')
  nameInput.value = name.value
})
</script>

<style scoped>
@import '@/assets/main.css';

.solution-overview {
  background: linear-gradient(135deg, #e8f5e8 0%, #f1f8e9 100%);
  padding: 1.5rem;
  border-radius: 8px;
  margin-bottom: 2rem;
  border: 2px solid #4CAF50;
}

.feature-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 0.5rem;
  margin-top: 1rem;
}

.feature-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.5rem;
}

.feature-item.completed .icon {
  color: #4CAF50;
  font-weight: bold;
}

.user-info,
.profile-section {
  background: #f8f9fa;
  padding: 1rem;
  border-radius: 8px;
  margin-bottom: 1rem;
}

.controls,
.profile-controls {
  display: flex;
  gap: 0.5rem;
  align-items: center;
  margin-top: 1rem;
  flex-wrap: wrap;
}

.input-field,
.select-field {
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

.btn-primary {
  background: #007bff;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.btn-primary:hover {
  background: #0056b3;
}

.btn-secondary {
  background: #6c757d;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.2s;
}

.btn-secondary:hover {
  background: #545b62;
}

.hobby-section {
  margin-top: 1rem;
  padding: 1rem;
  border: 1px solid #ddd;
  border-radius: 8px;
  background: #fff;
}

.hobby-controls {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.hobby-list {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.hobby-tag {
  background: #007bff;
  color: white;
  padding: 0.25rem 0.5rem;
  border-radius: 20px;
  font-size: 0.875rem;
  cursor: pointer;
  transition: background-color 0.2s;
}

.hobby-tag:hover {
  background: #dc3545;
}

.avatar {
  width: 50px;
  height: 50px;
  border-radius: 50%;
  vertical-align: middle;
}

.settings-section {
  margin-top: 1rem;
  padding: 1rem;
  border: 1px solid #ddd;
  border-radius: 8px;
  background: #fff;
}

.setting-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-bottom: 0.5rem;
}

.setting-item label {
  min-width: 60px;
  font-weight: 500;
}

.computed-demo {
  background: #f8f9fa;
  padding: 1rem;
  border-radius: 8px;
}

.user-card {
  background: white;
  padding: 1rem;
  border-radius: 8px;
  border: 1px solid #ddd;
  margin-top: 1rem;
}

.implementation-notes {
  margin-top: 2rem;
  padding: 1.5rem;
  background: #f8f9fa;
  border-radius: 8px;
}

.notes-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1rem;
  margin-top: 1rem;
}

.note-card {
  background: white;
  padding: 1rem;
  border-radius: 8px;
  border: 1px solid #ddd;
}

.note-card h4 {
  color: #007bff;
  margin-bottom: 0.5rem;
}

.note-card ul {
  margin: 0;
  padding-left: 1.2rem;
}

.note-card li {
  margin-bottom: 0.25rem;
  font-size: 0.9rem;
}
</style>
