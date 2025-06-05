<template>
  <div class="answering-area">
    <h2>🎯 實作練習區 - Lifecycle 生命週期</h2>
    <p class="description">
      📝 <strong>任務：</strong>建立一個整合計時器和資料載入的應用，實作各種生命週期鉤子
    </p>

    <!-- 任務一：計時器功能 -->
    <div class="task-section">
      <h3>⏰ 任務一：多功能計時器</h3>
      <div class="timer-container">
        <div class="timer-display">
          <h4>運行時間：{{ formatTime(elapsedTime) }}</h4>
          <p>狀態：{{ timerStatus }}</p>
        </div>

        <div class="timer-controls">
          <button @click="startTimer" :disabled="isRunning" class="btn btn-success">開始</button>
          <button @click="pauseTimer" :disabled="!isRunning" class="btn btn-warning">暫停</button>
          <button @click="resetTimer" class="btn btn-danger">重置</button>
        </div>

        <div class="timer-stats">
          <p>總啟動次數：{{ startCount }}</p>
          <p>總暫停次數：{{ pauseCount }}</p>
          <p>最長運行時間：{{ formatTime(maxRunTime) }}</p>
        </div>
      </div>
    </div>

    <!-- 任務二：資料載入 -->
    <div class="task-section">
      <h3>📡 任務二：資料載入管理</h3>
      <div class="data-container">
        <div class="loading-controls">
          <button @click="loadUserData" :disabled="isLoading" class="btn btn-primary">載入用戶資料</button>
          <button @click="loadNewsData" :disabled="isLoading" class="btn btn-primary">載入新聞資料</button>
          <button @click="clearData" class="btn btn-secondary">清空資料</button>
        </div>

        <div v-if="isLoading" class="loading-indicator">
          <p>載入中... {{ loadingProgress }}%</p>
          <div class="progress-bar">
            <div class="progress-fill" :style="{ width: loadingProgress + '%' }"></div>
          </div>
        </div>

        <div v-if="error" class="error-message">
          <p>❌ 載入失敗：{{ error }}</p>
          <button @click="retryLoad" class="btn btn-warning">重試</button>
        </div>

        <div v-if="userData.length > 0" class="data-display">
          <h4>👥 用戶資料 ({{ userData.length }} 筆)</h4>
          <div class="user-list">
            <!-- 🎯 任務：在這裡渲染用戶資料 -->
            <!--
            <div v-for="user in userData" :key="user.id" class="user-card">
              <h5>{{ user.name }}</h5>
              <p>{{ user.email }}</p>
            </div>
            -->
          </div>
        </div>

        <div v-if="newsData.length > 0" class="data-display">
          <h4>📰 新聞資料 ({{ newsData.length }} 筆)</h4>
          <div class="news-list">
            <!-- 🎯 任務：在這裡渲染新聞資料 -->
            <!--
            <div v-for="news in newsData" :key="news.id" class="news-card">
              <h5>{{ news.title }}</h5>
              <p>{{ news.summary }}</p>
            </div>
            -->
          </div>
        </div>
      </div>
    </div>

    <!-- 任務三：生命週期日誌 -->
    <div class="task-section">
      <h3>📝 任務三：生命週期追蹤</h3>
      <div class="lifecycle-log">
        <h4>生命週期事件日誌：</h4>
        <div class="log-container">
          <div v-for="(log, index) in lifecycleLogs" :key="index" class="log-entry">
            <span class="log-time">{{ log.time }}</span>
            <span class="log-event">{{ log.event }}</span>
            <span class="log-detail">{{ log.detail }}</span>
          </div>
        </div>
        <button @click="clearLogs" class="btn btn-secondary">清空日誌</button>
      </div>
    </div>

    <!-- 開發提示 -->
    <div class="hint-section">
      <h4>💡 開發提示</h4>
      <ul>
        <li>onMounted: 組件掛載時初始化計時器和載入初始資料</li>
        <li>onBeforeUnmount: 組件銷毀前清理計時器和事件監聽</li>
        <li>watch: 監聽資料變化並記錄到日誌</li>
        <li>計時器使用 setInterval，記得在適當時機清除</li>
        <li>模擬 API 載入可以使用 setTimeout 和 Promise</li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, watch } from 'vue'

// 計時器相關狀態
const elapsedTime = ref(0)
const isRunning = ref(false)
// eslint-disable-next-line no-unused-vars
const timerInterval = ref(null)
const startCount = ref(0)
const pauseCount = ref(0)
const maxRunTime = ref(0)
const timerStatus = ref('已停止')

// 資料載入相關狀態
const isLoading = ref(false)
const loadingProgress = ref(0)
const error = ref('')
const userData = ref([])
const newsData = ref([])

// 生命週期日誌
const lifecycleLogs = ref([])

// 🎯 任務：實作 addLifecycleLog 方法
// eslint-disable-next-line no-unused-vars
const addLifecycleLog = (event, detail = '') => {
  // 請在這裡實作新增生命週期日誌的邏輯
  // 格式：{ time: 當前時間, event: 事件名稱, detail: 詳細資訊 }
  console.log('請實作新增生命週期日誌功能')
}

// 🎯 任務：實作 formatTime 方法
// eslint-disable-next-line no-unused-vars
const formatTime = (seconds) => {
  // 請在這裡實作時間格式化邏輯
  // 將秒數轉換為 MM:SS 格式
  return '00:00'
}

// 🎯 任務：實作 startTimer 方法
const startTimer = () => {
  // 請在這裡實作開始計時器的邏輯
  // 1. 設定 isRunning 為 true
  // 2. 增加 startCount
  // 3. 使用 setInterval 每秒更新 elapsedTime
  // 4. 更新 timerStatus
  console.log('請實作開始計時器功能')
}

// 🎯 任務：實作 pauseTimer 方法
const pauseTimer = () => {
  // 請在這裡實作暫停計時器的邏輯
  // 1. 設定 isRunning 為 false
  // 2. 增加 pauseCount
  // 3. 清除 timerInterval
  // 4. 更新 timerStatus
  console.log('請實作暫停計時器功能')
}

// 🎯 任務：實作 resetTimer 方法
const resetTimer = () => {
  // 請在這裡實作重置計時器的邏輯
  // 1. 暫停計時器
  // 2. 重置 elapsedTime 為 0
  // 3. 更新最長運行時間
  // 4. 更新 timerStatus
  console.log('請實作重置計時器功能')
}

// 🎯 任務：實作 loadUserData 方法
const loadUserData = async () => {
  // 請在這裡實作載入用戶資料的邏輯
  // 1. 設定載入狀態
  // 2. 模擬 API 載入過程（使用 setTimeout）
  // 3. 更新載入進度
  // 4. 設定用戶資料
  console.log('請實作載入用戶資料功能')
}

// 🎯 任務：實作 loadNewsData 方法
const loadNewsData = async () => {
  // 請在這裡實作載入新聞資料的邏輯
  // 類似 loadUserData，但載入新聞資料
  console.log('請實作載入新聞資料功能')
}

// 🎯 任務：實作 clearData 方法
const clearData = () => {
  // 請在這裡實作清空資料的邏輯
  // 清空 userData 和 newsData
  console.log('請實作清空資料功能')
}

// 🎯 任務：實作 retryLoad 方法
const retryLoad = () => {
  // 請在這裡實作重試載入的邏輯
  // 清除錯誤狀態並重新載入
  console.log('請實作重試載入功能')
}

// 🎯 任務：實作 clearLogs 方法
const clearLogs = () => {
  // 請在這裡實作清空日誌的邏輯
  console.log('請實作清空日誌功能')
}

// 🎯 任務：實作 onMounted 生命週期鉤子
onMounted(() => {
  // 請在這裡實作組件掛載時的邏輯
  // 1. 記錄生命週期日誌
  // 2. 初始化計時器
  // 3. 載入初始資料
  console.log('請實作 onMounted 邏輯')
})

// 🎯 任務：實作 onBeforeUnmount 生命週期鉤子
onBeforeUnmount(() => {
  // 請在這裡實作組件銷毀前的邏輯
  // 1. 清除計時器
  // 2. 記錄生命週期日誌
  console.log('請實作 onBeforeUnmount 邏輯')
})

// 🎯 任務：實作 watch 監聽器
// 監聽 elapsedTime 的變化
// eslint-disable-next-line no-unused-vars
watch(elapsedTime, (newTime, oldTime) => {
  // 請在這裡實作監聽邏輯
  // 當時間變化時記錄到日誌
  console.log('請實作 watch 邏輯')
})
</script>

<style scoped>
.answering-area {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

.task-section {
  background: #f8f9fa;
  padding: 2rem;
  border-radius: 8px;
  margin: 2rem 0;
  border-left: 4px solid #17a2b8;
}

.timer-container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 2rem;
  align-items: start;
}

.timer-display {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  text-align: center;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.timer-display h4 {
  font-size: 1.5rem;
  color: #17a2b8;
  margin: 0;
}

.timer-controls {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.timer-stats {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.data-container {
  space-y: 1rem;
}

.loading-controls {
  display: flex;
  gap: 1rem;
  margin-bottom: 1rem;
  flex-wrap: wrap;
}

.loading-indicator {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.progress-bar {
  width: 100%;
  height: 20px;
  background: #e9ecef;
  border-radius: 10px;
  overflow: hidden;
  margin-top: 1rem;
}

.progress-fill {
  height: 100%;
  background: #28a745;
  transition: width 0.3s ease;
}

.error-message {
  background: #f8d7da;
  color: #721c24;
  padding: 1rem;
  border-radius: 8px;
  border: 1px solid #f5c6cb;
}

.data-display {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  margin: 1rem 0;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.user-list,
.news-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1rem;
  margin-top: 1rem;
}

.user-card,
.news-card {
  background: #f8f9fa;
  padding: 1rem;
  border-radius: 8px;
  border-left: 4px solid #007bff;
}

.lifecycle-log {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.log-container {
  max-height: 300px;
  overflow-y: auto;
  border: 1px solid #e9ecef;
  border-radius: 4px;
  padding: 1rem;
  margin: 1rem 0;
}

.log-entry {
  display: grid;
  grid-template-columns: 80px 120px 1fr;
  gap: 1rem;
  padding: 0.5rem 0;
  border-bottom: 1px solid #f1f3f4;
  font-family: monospace;
  font-size: 0.9rem;
}

.log-time {
  color: #6c757d;
}

.log-event {
  color: #007bff;
  font-weight: bold;
}

.log-detail {
  color: #495057;
}

.btn {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9rem;
}

.btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.btn-primary {
  background: #007bff;
  color: white;
}

.btn-secondary {
  background: #6c757d;
  color: white;
}

.btn-success {
  background: #28a745;
  color: white;
}

.btn-warning {
  background: #ffc107;
  color: black;
}

.btn-danger {
  background: #dc3545;
  color: white;
}

.hint-section {
  background: #fff3cd;
  padding: 1.5rem;
  border-radius: 8px;
  margin-top: 2rem;
  border-left: 4px solid #ffc107;
}

.hint-section ul {
  margin: 0.5rem 0;
  padding-left: 1.5rem;
}

.hint-section li {
  margin-bottom: 0.5rem;
}

@media (max-width: 768px) {
  .timer-container {
    grid-template-columns: 1fr;
  }

  .loading-controls {
    flex-direction: column;
  }

  .log-entry {
    grid-template-columns: 1fr;
    gap: 0.5rem;
  }
}
</style>
