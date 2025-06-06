<template>
  <div class="answering-area">
    <h2>🎯 參考答案 - Lifecycle 生命週期</h2>
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
            <div v-for="user in userData" :key="user.id" class="user-card">
              <h5>{{ user.name }}</h5>
              <p>{{ user.email }}</p>
              <small>部門：{{ user.department }}</small>
            </div>
          </div>
        </div>

        <div v-if="newsData.length > 0" class="data-display">
          <h4>📰 新聞資料 ({{ newsData.length }} 筆)</h4>
          <div class="news-list">
            <div v-for="news in newsData" :key="news.id" class="news-card">
              <h5>{{ news.title }}</h5>
              <p>{{ news.summary }}</p>
              <small>發布時間：{{ news.publishDate }}</small>
            </div>
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
const lastLoadType = ref('')

// 生命週期日誌
const lifecycleLogs = ref([])

// 新增生命週期日誌
const addLifecycleLog = (event, detail = '') => {
  const now = new Date()
  const time = now.toLocaleTimeString()
  lifecycleLogs.value.push({
    time,
    event,
    detail
  })

  // 限制日誌數量，避免記憶體溢出
  if (lifecycleLogs.value.length > 50) {
    lifecycleLogs.value.shift()
  }
}

// 時間格式化
const formatTime = (seconds) => {
  const minutes = Math.floor(seconds / 60)
  const secs = seconds % 60
  return `${minutes.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`
}

// 開始計時器
const startTimer = () => {
  if (!isRunning.value) {
    isRunning.value = true
    startCount.value++
    timerStatus.value = '運行中'

    timerInterval.value = setInterval(() => {
      elapsedTime.value++
    }, 1000)

    addLifecycleLog('TIMER_START', `第 ${startCount.value} 次啟動`)
  }
}

// 暫停計時器
const pauseTimer = () => {
  if (isRunning.value) {
    isRunning.value = false
    pauseCount.value++
    timerStatus.value = '已暫停'

    if (timerInterval.value) {
      clearInterval(timerInterval.value)
      timerInterval.value = null
    }

    addLifecycleLog('TIMER_PAUSE', `第 ${pauseCount.value} 次暫停`)
  }
}

// 重置計時器
const resetTimer = () => {
  // 先暫停計時器
  if (isRunning.value) {
    pauseTimer()
  }

  // 更新最長運行時間
  if (elapsedTime.value > maxRunTime.value) {
    maxRunTime.value = elapsedTime.value
  }

  // 重置時間
  elapsedTime.value = 0
  timerStatus.value = '已重置'

  addLifecycleLog('TIMER_RESET', `最長運行: ${formatTime(maxRunTime.value)}`)
}

// 模擬載入進度
const simulateLoading = (duration = 3000) => {
  return new Promise((resolve, reject) => {
    loadingProgress.value = 0
    const interval = setInterval(() => {
      loadingProgress.value += 10

      if (loadingProgress.value >= 100) {
        clearInterval(interval)
        // 隨機決定是否失敗
        if (Math.random() < 0.1) { // 10% 失敗率
          reject(new Error('網路連線超時'))
        } else {
          resolve()
        }
      }
    }, duration / 10)
  })
}

// 載入用戶資料
const loadUserData = async () => {
  if (isLoading.value) return

  isLoading.value = true
  lastLoadType.value = 'user'
  error.value = ''

  try {
    addLifecycleLog('DATA_LOAD_START', '開始載入用戶資料')

    await simulateLoading(2000)

    // 模擬用戶資料
    userData.value = [
      { id: 1, name: '張小明', email: 'zhang@example.com', department: '技術部' },
      { id: 2, name: '李小華', email: 'li@example.com', department: '行銷部' },
      { id: 3, name: '王小美', email: 'wang@example.com', department: '人事部' },
      { id: 4, name: '陳小強', email: 'chen@example.com', department: '財務部' }
    ]

    addLifecycleLog('DATA_LOAD_SUCCESS', `載入 ${userData.value.length} 筆用戶資料`)

  } catch (err) {
    error.value = err.message
    addLifecycleLog('DATA_LOAD_ERROR', `載入失敗: ${err.message}`)
  } finally {
    isLoading.value = false
    loadingProgress.value = 0
  }
}

// 載入新聞資料
const loadNewsData = async () => {
  if (isLoading.value) return

  isLoading.value = true
  lastLoadType.value = 'news'
  error.value = ''

  try {
    addLifecycleLog('DATA_LOAD_START', '開始載入新聞資料')

    await simulateLoading(2500)

    // 模擬新聞資料
    newsData.value = [
      {
        id: 1,
        title: 'Vue 3.4 正式發布',
        summary: '帶來更好的效能和開發體驗...',
        publishDate: '2024-01-15'
      },
      {
        id: 2,
        title: 'JavaScript 新特性解析',
        summary: '深入了解最新的 ES2024 特性...',
        publishDate: '2024-01-14'
      },
      {
        id: 3,
        title: '前端開發趨勢展望',
        summary: '探討 2024 年前端技術發展方向...',
        publishDate: '2024-01-13'
      }
    ]

    addLifecycleLog('DATA_LOAD_SUCCESS', `載入 ${newsData.value.length} 筆新聞資料`)

  } catch (err) {
    error.value = err.message
    addLifecycleLog('DATA_LOAD_ERROR', `載入失敗: ${err.message}`)
  } finally {
    isLoading.value = false
    loadingProgress.value = 0
  }
}

// 清空資料
const clearData = () => {
  userData.value = []
  newsData.value = []
  error.value = ''
  addLifecycleLog('DATA_CLEAR', '清空所有資料')
}

// 重試載入
const retryLoad = () => {
  error.value = ''
  if (lastLoadType.value === 'user') {
    loadUserData()
  } else if (lastLoadType.value === 'news') {
    loadNewsData()
  }
}

// 清空日誌
const clearLogs = () => {
  lifecycleLogs.value = []
  addLifecycleLog('LOG_CLEAR', '清空生命週期日誌')
}

// 組件掛載時
onMounted(() => {
  addLifecycleLog('MOUNTED', '組件已掛載')

  // 初始化應用
  timerStatus.value = '已停止'

  // 載入一些初始資料
  setTimeout(() => {
    addLifecycleLog('INIT_COMPLETE', '應用初始化完成')
  }, 100)
})

// 組件銷毀前
onBeforeUnmount(() => {
  addLifecycleLog('BEFORE_UNMOUNT', '組件即將銷毀')

  // 清理計時器
  if (timerInterval.value) {
    clearInterval(timerInterval.value)
    timerInterval.value = null
  }

  // 記錄最終狀態
  addLifecycleLog('CLEANUP', `最終運行時間: ${formatTime(elapsedTime.value)}`)
})

// 監聽計時器時間變化
watch(elapsedTime, (newTime, oldTime) => {
  // 每 30 秒記錄一次
  if (newTime > 0 && newTime % 30 === 0) {
    addLifecycleLog('TIMER_MILESTONE', `運行已達 ${formatTime(newTime)}`)
  }
})

// 監聽資料載入狀態
watch(isLoading, (newStatus, oldStatus) => {
  if (newStatus !== oldStatus) {
    addLifecycleLog('LOADING_STATUS', newStatus ? '開始載入' : '載入結束')
  }
})

// 監聽用戶資料變化
watch(userData, (newData) => {
  if (newData.length > 0) {
    addLifecycleLog('USER_DATA_UPDATE', `用戶資料已更新，共 ${newData.length} 筆`)
  }
}, { deep: true })

// 監聽新聞資料變化
watch(newsData, (newData) => {
  if (newData.length > 0) {
    addLifecycleLog('NEWS_DATA_UPDATE', `新聞資料已更新，共 ${newData.length} 筆`)
  }
}, { deep: true })
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
  transition: transform 0.2s;
}

.user-card:hover,
.news-card:hover {
  transform: translateY(-2px);
}

.user-card h5,
.news-card h5 {
  margin: 0 0 0.5rem 0;
  color: #343a40;
}

.user-card p,
.news-card p {
  margin: 0.25rem 0;
  color: #6c757d;
}

.user-card small,
.news-card small {
  color: #6c757d;
  font-size: 0.875rem;
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
  background: #f8f9fa;
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

.log-entry:last-child {
  border-bottom: none;
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
  transition: all 0.2s;
}

.btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.btn-primary {
  background: #007bff;
  color: white;
}

.btn-primary:hover:not(:disabled) {
  background: #0056b3;
}

.btn-secondary {
  background: #6c757d;
  color: white;
}

.btn-secondary:hover:not(:disabled) {
  background: #545b62;
}

.btn-success {
  background: #28a745;
  color: white;
}

.btn-success:hover:not(:disabled) {
  background: #1e7e34;
}

.btn-warning {
  background: #ffc107;
  color: black;
}

.btn-warning:hover:not(:disabled) {
  background: #e0a800;
}

.btn-danger {
  background: #dc3545;
  color: white;
}

.btn-danger:hover:not(:disabled) {
  background: #c82333;
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
