<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - Lifecycle 生命週期</h2>
    <p class="route-info">📍 路徑：/LifecycleSamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>挑戰任務：</strong>練習 Vue3 生命週期鉤子的基本用法
    </p>

    <!-- 任務說明區塊 -->
    <div class="task-instructions">
      <h3>📋 學員任務清單</h3>
      <div class="instruction-card">
        <h4>🎯 任務一：實作基本計時器 (onMounted & onUnmounted)</h4>
        <div class="task-details">
          <p><strong>目標：</strong>練習組件掛載和卸載時的資源管理</p>
          <ul>
            <li><strong>在 onMounted 中：</strong>啟動一個每秒更新的計時器</li>
            <li><strong>在 onUnmounted 中：</strong>清理計時器，避免記憶體洩漏</li>
            <li><strong>實作 formatTime() 函數：</strong>將秒數轉換為 "mm:ss" 格式</li>
            <li><strong>實作 toggleTimer() 函數：</strong>控制計時器的開始和暫停</li>
          </ul>
          <div class="logic-spec">
            <strong>邏輯規格：</strong>
            <pre>formatTime(90) → "01:30"
toggleTimer() → 如果正在運行則暫停，否則開始</pre>
          </div>
        </div>
      </div>

      <div class="instruction-card">
        <h4>🎯 任務二：組件更新監控 (onUpdated)</h4>
        <div class="task-details">
          <p><strong>目標：</strong>學習監控組件的更新行為</p>
          <ul>
            <li><strong>在 onUpdated 中：</strong>每次組件更新時增加計數器</li>
            <li><strong>實作 incrementCounter() 函數：</strong>手動觸發計數器增加</li>
            <li><strong>觀察更新行為：</strong>了解什麼操作會觸發組件更新</li>
          </ul>
          <div class="logic-spec">
            <strong>邏輯規格：</strong>
            <pre>每次組件重新渲染 → updateCount 自動 +1
點擊按鈕 → counter 手動 +1</pre>
          </div>
        </div>
      </div>

      <div class="instruction-card">
        <h4>🎯 任務三：模擬數據載入</h4>
        <div class="task-details">
          <p><strong>目標：</strong>結合生命週期和異步操作</p>
          <ul>
            <li><strong>實作 loadUserData() 函數：</strong>模擬 API 數據載入</li>
            <li><strong>處理載入狀態：</strong>顯示載入中、成功、失敗狀態</li>
            <li><strong>在適當時機：</strong>選擇在 onMounted 或手動觸發載入</li>
          </ul>
          <div class="logic-spec">
            <strong>邏輯規格：</strong>
            <pre>載入中 → loading = true, 顯示載入提示
2秒後 → 返回模擬用戶數據
載入完成 → loading = false, 顯示數據</pre>
          </div>
        </div>
      </div>
    </div>

    <!-- 實作區域 -->
    <div class="demo-section">
      <h3>⏰ 任務一：基本計時器</h3>
      <div class="timer-section">
        <div class="timer-display">
          <h4>運行時間：{{ formatTime(elapsedTime) }}</h4>
          <p>狀態：{{ isRunning ? '🟢 運行中' : '🔴 已暫停' }}</p>
        </div>
        <div class="timer-controls">
          <!-- TODO: 連接 toggleTimer 函數 -->
          <button @click="toggleTimer" class="btn btn-primary">
            {{ isRunning ? '⏸️ 暫停' : '▶️ 開始' }}
          </button>
        </div>
      </div>
    </div>

    <div class="demo-section">
      <h3>📊 任務二：更新監控</h3>
      <div class="update-section">
        <div class="counter-display">
          <p>手動計數器：<span class="counter-value">{{ counter }}</span></p>
          <p>組件更新次數：<span class="update-value">{{ updateCount }}</span></p>
        </div>
        <div class="update-controls">
          <!-- TODO: 實作 incrementCounter 函數 -->
          <button @click="incrementCounter" class="btn btn-success">
            🔢 增加計數器
          </button>
          <small class="help-text">點擊按鈕觀察組件更新行為</small>
        </div>
      </div>
    </div>

    <div class="demo-section">
      <h3>📡 任務三：數據載入</h3>
      <div class="data-section">
        <div class="loading-controls">
          <!-- TODO: 實作 loadUserData 函數 -->
          <button @click="loadUserData" class="btn btn-info" :disabled="loading">
            {{ loading ? '📡 載入中...' : '🔄 載入用戶數據' }}
          </button>
        </div>

        <div v-if="loading" class="loading-status">
          <div class="loading-spinner">⏳ 正在載入數據...</div>
        </div>

        <div v-if="!loading && userData.length > 0" class="user-data">
          <h4>👥 用戶列表：</h4>
          <div class="user-list">
            <div v-for="user in userData" :key="user.id" class="user-item">
              {{ user.name }} ({{ user.email }})
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="status-section">
      <h3>🔍 組件狀態監控</h3>
      <div class="status-grid">
        <div class="status-item">
          <strong>計時器：</strong>
          <span :class="{ active: isRunning }">{{ isRunning ? '運行中' : '已停止' }}</span>
        </div>
        <div class="status-item">
          <strong>更新次數：</strong>
          <span>{{ updateCount }} 次</span>
        </div>
        <div class="status-item">
          <strong>數據狀態：</strong>
          <span>{{ loading ? '載入中' : userData.length > 0 ? '已載入' : '未載入' }}</span>
        </div>
      </div>
    </div>

    <div class="hint-section">
      <h4>💡 實作提示</h4>
      <details>
        <summary>點擊查看生命週期鉤子用法</summary>
        <pre><code>// 1. 匯入生命週期鉤子
import { onMounted, onUnmounted, onUpdated } from 'vue'

// 2. 在 onMounted 中初始化
onMounted(() => {
  console.log('組件已掛載')
  // 啟動計時器的程式碼...
})

// 3. 在 onUnmounted 中清理
onUnmounted(() => {
  console.log('組件即將卸載')
  // 清理計時器的程式碼...
})

// 4. 在 onUpdated 中監控更新
onUpdated(() => {
  console.log('組件已更新')
  // 更新計數的程式碼...
})</code></pre>
      </details>

      <details>
        <summary>點擊查看函數實作提示</summary>
        <pre><code>// formatTime 實作提示
const formatTime = (seconds) => {
  const mins = Math.floor(seconds / 60)
  const secs = seconds % 60
  // 回傳格式化字串...
}

// 計時器控制提示
const toggleTimer = () => {
  if (isRunning.value) {
    // 停止計時器...
  } else {
    // 啟動計時器...
  }
}

// 數據載入提示
const loadUserData = async () => {
  loading.value = true
  // 模擬 API 延遲...
  // 設定模擬數據...
  loading.value = false
}</code></pre>
      </details>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, onUpdated } from 'vue'

// 任務一：計時器相關
const elapsedTime = ref(0)
const isRunning = ref(false)
// eslint-disable-next-line no-unused-vars
const timer = ref(null)

// 任務二：更新監控相關
const counter = ref(0)
const updateCount = ref(0)

// 任務三：數據載入相關
const userData = ref([])
const loading = ref(false)

// TODO: 學員需要實作以下函數

// 任務一：格式化時間顯示 (例：90秒 → "01:30")
const formatTime = () => {
  // 請在這裡實作時間格式化邏輯
  // 提示：使用 Math.floor 和 % 運算符，參數為 elapsedTime.value
  return '00:00'
}

// 任務一：切換計時器狀態
const toggleTimer = () => {
  // 請在這裡實作計時器開始/暫停邏輯
  // 提示：使用 setInterval 和 clearInterval
}

// 任務二：增加手動計數器
const incrementCounter = () => {
  // 請在這裡實作計數器增加邏輯
  // 提示：這會觸發組件更新
}

// 任務三：載入用戶數據
const loadUserData = async () => {
  // 請在這裡實作數據載入邏輯
  // 提示：設定 loading 狀態，使用 setTimeout 模擬延遲
  // 模擬數據結構：[{ id: 1, name: '張三', email: 'zhang@example.com' }]
}

// TODO: 學員需要實作以下生命週期鉤子

onMounted(() => {
  // 請在這裡實作組件掛載後的邏輯
  // 任務：可以選擇自動啟動計時器或載入數據
})

onUnmounted(() => {
  // 請在這裡實作組件卸載前的清理邏輯
  // 任務：清理計時器，避免記憶體洩漏
})

onUpdated(() => {
  // 請在這裡實作組件更新後的邏輯
  // 任務：增加更新計數器
})
</script>

<style scoped>
.self-challenge {
  max-width: 1000px;
  margin: 0 auto;
  padding: 2rem;
}

.route-info {
  background: #e3f2fd;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  margin: 1rem 0;
  font-family: monospace;
}

.description {
  font-size: 1.1rem;
  margin: 1.5rem 0;
}

.task-instructions {
  background: #fff8e1;
  padding: 1.5rem;
  border-radius: 8px;
  margin: 2rem 0;
  border-left: 4px solid #ffc107;
}

.instruction-card {
  background: white;
  margin: 1rem 0;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.instruction-card h4 {
  color: #1976d2;
  margin-bottom: 1rem;
}

.task-details ul {
  margin: 1rem 0;
  padding-left: 1.5rem;
}

.task-details li {
  margin: 0.5rem 0;
  line-height: 1.6;
}

.logic-spec {
  background: #f5f5f5;
  padding: 1rem;
  border-radius: 4px;
  margin-top: 1rem;
}

.logic-spec pre {
  margin: 0.5rem 0 0 0;
  font-size: 0.9rem;
  color: #2e7d32;
}

.demo-section {
  margin: 2rem 0;
  padding: 1.5rem;
  border: 1px solid #ddd;
  border-radius: 8px;
  background: #fafafa;
}

.timer-section,
.update-section,
.data-section {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.timer-display,
.counter-display {
  background: white;
  padding: 1rem;
  border-radius: 8px;
  border: 1px solid #e0e0e0;
}

.timer-display h4 {
  font-size: 1.5rem;
  color: #1976d2;
  margin: 0.5rem 0;
}

.counter-value,
.update-value {
  font-size: 1.2rem;
  font-weight: bold;
  color: #4caf50;
}

.timer-controls,
.update-controls,
.loading-controls {
  display: flex;
  gap: 1rem;
  align-items: center;
}

.help-text {
  color: #666;
  font-style: italic;
}

.loading-status {
  text-align: center;
  padding: 2rem;
}

.loading-spinner {
  font-size: 1.2rem;
  color: #ff9800;
  animation: pulse 1.5s ease-in-out infinite alternate;
}

@keyframes pulse {
  from {
    opacity: 1;
  }

  to {
    opacity: 0.5;
  }
}

.user-data {
  background: white;
  padding: 1rem;
  border-radius: 8px;
  border: 1px solid #e0e0e0;
}

.user-list {
  margin-top: 1rem;
}

.user-item {
  padding: 0.5rem;
  background: #f8f9fa;
  margin: 0.5rem 0;
  border-radius: 4px;
  border-left: 3px solid #4caf50;
}

.status-section {
  background: #e8f5e8;
  padding: 1.5rem;
  border-radius: 8px;
  margin: 2rem 0;
}

.status-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
  margin-top: 1rem;
}

.status-item {
  background: white;
  padding: 1rem;
  border-radius: 8px;
  border: 1px solid #c8e6c9;
}

.status-item .active {
  color: #4caf50;
  font-weight: bold;
}

.btn {
  padding: 0.6rem 1.2rem;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-size: 0.9rem;
  font-weight: 500;
  transition: all 0.2s;
}

.btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.btn-primary {
  background: #1976d2;
  color: white;
}

.btn-success {
  background: #4caf50;
  color: white;
}

.btn-info {
  background: #00bcd4;
  color: white;
}

.btn:hover:not(:disabled) {
  transform: translateY(-1px);
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.15);
}

.hint-section {
  background: #e8f5e8;
  padding: 1.5rem;
  border-radius: 8px;
  margin: 2rem 0;
}

details {
  margin: 1rem 0;
}

summary {
  cursor: pointer;
  font-weight: bold;
  padding: 0.8rem;
  background: #c8e6c9;
  border-radius: 4px;
  transition: background-color 0.2s;
}

summary:hover {
  background: #a5d6a7;
}

pre {
  background: #2d3748;
  color: #e2e8f0;
  padding: 1rem;
  border-radius: 4px;
  overflow-x: auto;
  margin-top: 1rem;
  line-height: 1.5;
}
</style>
