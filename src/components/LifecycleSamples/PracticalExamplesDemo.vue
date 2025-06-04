<!-- components/LifecycleSamples/PracticalExamplesDemo.vue -->
<template>
  <div class="practical-examples-demo">
    <h2>生命週期實際應用</h2>
    <p class="route-info">📍 路徑：/LifecycleSamples/PracticalExamplesDemo.vue</p>

    <!-- 計時器管理 -->
    <div class="demo-section">
      <h3>1. 計時器與資源管理</h3>
      <div class="controls">
        <button @click="toggleTimer" class="btn btn-primary">
          {{ timerRunning ? '停止' : '開始' }} 計時器
        </button>
        <button @click="resetTimer" class="btn btn-secondary">
          重置
        </button>
      </div>
      <div class="result">
        <div class="timer-display">
          <div class="timer-value">{{ formatTime(elapsedTime) }}</div>
          <div class="timer-status">
            狀態: {{ timerRunning ? '運行中' : '已停止' }}
          </div>
        </div>
        <div class="resource-info">
          <p><strong>資源管理說明：</strong></p>
          <ul>
            <li>在 onMounted 中啟動計時器</li>
            <li>在 onUnmounted 中清除計時器，防止記憶體洩漏</li>
            <li>組件銷毀時自動清理資源</li>
          </ul>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 計時器資源管理
import { ref, onMounted, onUnmounted } from 'vue'

const elapsedTime = ref(0)
const timerRunning = ref(false)
let timer = null

const startTimer = () => {
  if (!timer) {
    timer = setInterval(() => {
      elapsedTime.value++
    }, 1000)
    timerRunning.value = true
  }
}

const stopTimer = () => {
  if (timer) {
    clearInterval(timer)
    timer = null
    timerRunning.value = false
  }
}

onMounted(() => {
  // 組件掛載時可以啟動計時器
  console.log('計時器組件已掛載')
})

onUnmounted(() => {
  // ⚠️ 重要：組件卸載時必須清除計時器
  stopTimer()
  console.log('計時器已清除，防止記憶體洩漏')
})</code></pre>
      </div>
    </div>

    <!-- 事件監聽器 -->
    <div class="demo-section">
      <h3>2. 全域事件監聽器</h3>
      <div class="controls">
        <div class="event-info">
          <span>滑鼠位置: ({{ mouseX }}, {{ mouseY }})</span>
          <span>視窗大小: {{ windowWidth }} x {{ windowHeight }}</span>
        </div>
      </div>
      <div class="result">
        <div class="event-display">
          <div class="event-item">
            <h4>滑鼠追蹤</h4>
            <div class="mouse-tracker" @mousemove="onLocalMouseMove">
              <div class="mouse-pointer" :style="{ left: localMouseX + 'px', top: localMouseY + 'px' }"></div>
              <p>在此區域移動滑鼠</p>
            </div>
          </div>

          <div class="event-item">
            <h4>鍵盤事件</h4>
            <div class="keyboard-display">
              <div>最後按鍵: {{ lastKey || '無' }}</div>
              <div>按鍵次數: {{ keyPressCount }}</div>
            </div>
          </div>
        </div>

        <div class="event-logs">
          <h4>事件記錄 (最近 5 筆):</h4>
          <div class="log-list">
            <div v-for="(log, index) in recentEvents" :key="index" class="event-log">
              {{ log }}
            </div>
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 全域事件監聽器管理
import { ref, onMounted, onUnmounted } from 'vue'

const mouseX = ref(0)
const mouseY = ref(0)
const windowWidth = ref(0)
const windowHeight = ref(0)

const handleMouseMove = (event) => {
  mouseX.value = event.clientX
  mouseY.value = event.clientY
}

const handleResize = () => {
  windowWidth.value = window.innerWidth
  windowHeight.value = window.innerHeight
}

const handleKeyPress = (event) => {
  lastKey.value = event.key
  keyPressCount.value++
}

onMounted(() => {
  // 添加全域事件監聽器
  window.addEventListener('mousemove', handleMouseMove)
  window.addEventListener('resize', handleResize)
  window.addEventListener('keydown', handleKeyPress)

  // 初始化視窗大小
  handleResize()
})

onUnmounted(() => {
  // ⚠️ 重要：移除全域事件監聽器
  window.removeEventListener('mousemove', handleMouseMove)
  window.removeEventListener('resize', handleResize)
  window.removeEventListener('keydown', handleKeyPress)
})</code></pre>
      </div>
    </div>

    <!-- API 請求 -->
    <div class="demo-section">
      <h3>3. API 請求與載入狀態</h3>
      <div class="controls">
        <button @click="fetchUserData" class="btn btn-success" :disabled="loading">
          {{ loading ? '載入中...' : '重新載入用戶數據' }}
        </button>
        <button @click="simulateError" class="btn btn-warning">
          模擬錯誤
        </button>
      </div>
      <div class="result">
        <div class="api-status">
          <div class="status-item">
            <span>載入狀態:</span>
            <span :class="getStatusClass()">{{ getStatusText() }}</span>
          </div>
          <div class="status-item">
            <span>載入時間:</span>
            <span>{{ loadTime }}ms</span>
          </div>
        </div>

        <div class="api-content">
          <div v-if="loading" class="loading-state">
            <div class="spinner"></div>
            <p>正在載入用戶數據...</p>
          </div>

          <div v-else-if="error" class="error-state">
            <div class="error-icon">⚠️</div>
            <p>{{ error }}</p>
            <button @click="fetchUserData" class="btn btn-small">重試</button>
          </div>

          <div v-else-if="userData" class="success-state">
            <div class="user-card">
              <h4>{{ userData.name }}</h4>
              <p>Email: {{ userData.email }}</p>
              <p>部門: {{ userData.department }}</p>
              <p>加入時間: {{ userData.joinDate }}</p>
            </div>
          </div>

          <div v-else class="empty-state">
            點擊按鈕載入數據
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// API 請求生命週期管理
import { ref, onMounted } from 'vue'

const loading = ref(false)
const userData = ref(null)
const error = ref(null)

const fetchUserData = async () => {
  loading.value = true
  error.value = null

  try {
    const startTime = Date.now()

    // 模擬 API 請求
    const response = await fetch('/api/user')
    if (!response.ok) throw new Error('請求失敗')

    const data = await response.json()
    userData.value = data

    loadTime.value = Date.now() - startTime
  } catch (err) {
    error.value = err.message
  } finally {
    loading.value = false
  }
}

// ✅ 在組件掛載時自動載入初始數據
onMounted(() => {
  fetchUserData()
})</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// 計時器管理
const elapsedTime = ref(0)
const timerRunning = ref(false)
let timer = null

// 事件監聽器
const mouseX = ref(0)
const mouseY = ref(0)
const windowWidth = ref(0)
const windowHeight = ref(0)
const localMouseX = ref(0)
const localMouseY = ref(0)
const lastKey = ref('')
const keyPressCount = ref(0)
const recentEvents = ref([])

// API 請求
const loading = ref(false)
const userData = ref(null)
const error = ref(null)
const loadTime = ref(0)

// 生命週期
onMounted(() => {
  // 全域事件監聽器
  window.addEventListener('mousemove', handleMouseMove)
  window.addEventListener('resize', handleResize)
  window.addEventListener('keydown', handleKeyPress)

  // 初始化
  handleResize()

  // 自動載入數據
  fetchUserData()
})

onUnmounted(() => {
  // 清除計時器
  if (timer) {
    clearInterval(timer)
  }

  // 移除事件監聽器
  window.removeEventListener('mousemove', handleMouseMove)
  window.removeEventListener('resize', handleResize)
  window.removeEventListener('keydown', handleKeyPress)
})

// 計時器方法
const toggleTimer = () => {
  if (timerRunning.value) {
    stopTimer()
  } else {
    startTimer()
  }
}

const startTimer = () => {
  if (!timer) {
    timer = setInterval(() => {
      elapsedTime.value++
    }, 1000)
    timerRunning.value = true
  }
}

const stopTimer = () => {
  if (timer) {
    clearInterval(timer)
    timer = null
    timerRunning.value = false
  }
}

const resetTimer = () => {
  stopTimer()
  elapsedTime.value = 0
}

const formatTime = (seconds) => {
  const mins = Math.floor(seconds / 60)
  const secs = seconds % 60
  return `${mins.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`
}

// 事件處理
const handleMouseMove = (event) => {
  mouseX.value = event.clientX
  mouseY.value = event.clientY
  addEvent(`滑鼠移動: (${event.clientX}, ${event.clientY})`)
}

const handleResize = () => {
  windowWidth.value = window.innerWidth
  windowHeight.value = window.innerHeight
  addEvent(`視窗調整: ${window.innerWidth}x${window.innerHeight}`)
}

const handleKeyPress = (event) => {
  lastKey.value = event.key
  keyPressCount.value++
  addEvent(`按鍵: ${event.key}`)
}

const onLocalMouseMove = (event) => {
  const rect = event.currentTarget.getBoundingClientRect()
  localMouseX.value = event.clientX - rect.left
  localMouseY.value = event.clientY - rect.top
}

const addEvent = (eventText) => {
  recentEvents.value.unshift(`${new Date().toLocaleTimeString()} - ${eventText}`)
  if (recentEvents.value.length > 5) {
    recentEvents.value.pop()
  }
}

// API 請求方法
const fetchUserData = async () => {
  loading.value = true
  error.value = null

  try {
    const startTime = Date.now()

    // 模擬 API 請求延遲
    await new Promise(resolve => setTimeout(resolve, 1500))

    // 模擬用戶數據
    userData.value = {
      name: '張小明',
      email: 'zhang.xiaoming@company.com',
      department: '前端開發部',
      joinDate: '2023-01-15'
    }

    loadTime.value = Date.now() - startTime
  } catch (err) {
    error.value = err.message
  } finally {
    loading.value = false
  }
}

const simulateError = async () => {
  loading.value = true
  error.value = null
  userData.value = null

  try {
    await new Promise(resolve => setTimeout(resolve, 1000))
    throw new Error('網路連線失敗，請檢查網路設定')
  } catch (err) {
    error.value = err.message
  } finally {
    loading.value = false
  }
}

const getStatusClass = () => {
  if (loading.value) return 'status-loading'
  if (error.value) return 'status-error'
  if (userData.value) return 'status-success'
  return 'status-idle'
}

const getStatusText = () => {
  if (loading.value) return '載入中'
  if (error.value) return '錯誤'
  if (userData.value) return '成功'
  return '待載入'
}
</script>

<style scoped>
/* 樣式已在 src/assets/main.css 中定義 */
</style>
