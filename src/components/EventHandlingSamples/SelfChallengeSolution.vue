<template>
  <div class="self-challenge-solution">
    <h2>✅ 解答版本 - Event 事件處理</h2>
    <p class="route-info">📍 路徑：/EventHandlingSamples/SelfChallengeSolution.vue</p>
    <p class="description">
      📝 <strong>完整實作：</strong>互動計數器系統，展示各種事件處理技巧
    </p>

    <div class="counter-container">
      <!-- 主要計數顯示區域 -->
      <div class="counter-display" :class="{ 'double-clicked': isDoubleClicked }" @dblclick="handleDoubleClick">
        <div class="counter-value">{{ count }}</div>
        <div class="counter-label">互動計數器</div>
        <div class="counter-progress">
          <div class="progress-bar" :style="{ width: count + '%' }"></div>
        </div>
        <div class="counter-hint">雙擊快速增加 +5</div>
      </div>

      <!-- 控制按鈕區域 -->
      <div class="control-buttons">
        <button class="btn increment-btn" @click="increment" :disabled="count >= 100">
          ➕ 增加 (+1)
        </button>
        <button class="btn decrement-btn" @click="decrement" :disabled="count <= 0">
          ➖ 減少 (-1)
        </button>
        <button class="btn reset-btn" @click="reset">
          🔄 重置 (0)
        </button>
      </div>

      <!-- 鍵盤提示區域 -->
      <div class="keyboard-hints">
        <h4>⌨️ 鍵盤快捷鍵</h4>
        <div class="hint-grid">
          <div class="hint-item">
            <span>增加計數</span>
            <kbd>Space</kbd>
          </div>
          <div class="hint-item">
            <span>減少計數</span>
            <kbd>-</kbd>
          </div>
          <div class="hint-item">
            <span>重置計數</span>
            <kbd>R</kbd>
          </div>
        </div>
      </div>

      <!-- 目標設定表單 -->
      <div class="target-form">
        <h4>🎯 設定目標值</h4>
        <form @submit="handleSubmit" class="form-inline">
          <input type="number" v-model="targetValue" placeholder="輸入 0-100" min="0" max="100" class="target-input">
          <button type="submit" class="btn submit-btn">設定</button>
        </form>
      </div>

      <!-- 統計面板 -->
      <div class="stats-panel">
        <h4>📊 操作統計</h4>
        <div class="stats-grid">
          <div class="stat-item">
            <div class="stat-value">{{ count }}</div>
            <div class="stat-label">目前值</div>
          </div>
          <div class="stat-item">
            <div class="stat-value">{{ actionHistory.length }}</div>
            <div class="stat-label">操作次數</div>
          </div>
          <div class="stat-item">
            <div class="stat-value">{{ count }}%</div>
            <div class="stat-label">進度</div>
          </div>
          <div class="stat-item">
            <div class="stat-value">{{ 100 - count }}</div>
            <div class="stat-label">剩餘空間</div>
          </div>
        </div>
      </div>

      <!-- 操作歷史記錄 -->
      <div class="history-panel">
        <h4>📋 操作歷史</h4>
        <div class="history-list" v-if="actionHistory.length > 0">
          <div v-for="(action, index) in actionHistory.slice().reverse()" :key="index" class="history-item"
            :class="'action-' + action.action">
            <span class="action-icon">{{ getActionIcon(action.action) }}</span>
            <span class="action-text">{{ getActionText(action.action, action.value) }}</span>
            <span class="action-time">{{ action.time }}</span>
          </div>
        </div>
        <div v-else class="no-history">
          尚無操作記錄
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// 響應式數據
const count = ref(0)
const actionHistory = ref([])
const isDoubleClicked = ref(false)
const targetValue = ref('')

// 1. increment() - 增加計數器的值
const increment = () => {
  if (count.value < 100) {
    count.value += 1
    addActionLog('increment', count.value)
  }
}

// 2. decrement() - 減少計數器的值
const decrement = () => {
  if (count.value > 0) {
    count.value -= 1
    addActionLog('decrement', count.value)
  }
}

// 3. reset() - 重置計數器為 0
const reset = () => {
  count.value = 0
  actionHistory.value = []
  addActionLog('reset', 0)
}

// 4. handleKeydown(event) - 處理鍵盤按鍵事件
const handleKeydown = (event) => {
  switch (event.key) {
    case ' ': // Space 鍵
      event.preventDefault()
      increment()
      break
    case 'r':
    case 'R':
      event.preventDefault()
      reset()
      break
    case '-':
      event.preventDefault()
      decrement()
      break
  }
}

// 5. handleDoubleClick() - 處理雙擊事件
const handleDoubleClick = () => {
  const newValue = Math.min(count.value + 5, 100)
  count.value = newValue
  addActionLog('double-click', newValue)

  // 視覺回饋
  isDoubleClicked.value = true
  setTimeout(() => {
    isDoubleClicked.value = false
  }, 1000)
}

// 6. handleSubmit(event) - 處理表單提交事件
const handleSubmit = (event) => {
  event.preventDefault()

  const value = parseInt(targetValue.value)

  // 驗證輸入值
  if (isNaN(value) || value < 0 || value > 100) {
    alert('請輸入有效的數字 (0-100)')
    return
  }

  count.value = value
  targetValue.value = ''
  addActionLog('set-target', value)
}

// 輔助函數：添加操作日誌
const addActionLog = (action, value) => {
  actionHistory.value.push({
    action,
    value,
    time: new Date().toLocaleTimeString()
  })
}

// 輔助函數：獲取操作圖標
const getActionIcon = (action) => {
  const icons = {
    'increment': '➕',
    'decrement': '➖',
    'reset': '🔄',
    'double-click': '⚡',
    'set-target': '🎯'
  }
  return icons[action] || '📝'
}

// 輔助函數：獲取操作文字
const getActionText = (action, value) => {
  const texts = {
    'increment': `增加到 ${value}`,
    'decrement': `減少到 ${value}`,
    'reset': '重置計數器',
    'double-click': `快速增加到 ${value}`,
    'set-target': `設定目標值為 ${value}`
  }
  return texts[action] || `操作: ${action}`
}

// 7. 生命週期設定 - 設定全域鍵盤事件監聽器
onMounted(() => {
  document.addEventListener('keydown', handleKeydown)
})

onUnmounted(() => {
  document.removeEventListener('keydown', handleKeydown)
})
</script>

<style scoped>
.self-challenge-solution {
  max-width: 1000px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.route-info {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 8px 16px;
  border-radius: 20px;
  font-size: 14px;
  display: inline-block;
  margin-bottom: 20px;
}

.description {
  color: #555;
  margin-bottom: 30px;
  font-size: 16px;
}

.counter-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
  align-items: start;
}

.counter-display {
  grid-column: 1 / -1;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 40px;
  border-radius: 20px;
  text-align: center;
  margin-bottom: 20px;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
  cursor: pointer;
  user-select: none;
}

.counter-display:hover {
  transform: scale(1.02);
  box-shadow: 0 10px 25px rgba(102, 126, 234, 0.3);
}

.counter-display.double-clicked {
  transform: scale(1.05);
  box-shadow: 0 0 30px rgba(102, 126, 234, 0.5);
}

.counter-value {
  font-size: 4rem;
  font-weight: bold;
  margin-bottom: 10px;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}

.counter-label {
  font-size: 1.2rem;
  opacity: 0.9;
  margin-bottom: 20px;
}

.counter-progress {
  width: 100%;
  height: 8px;
  background: rgba(255, 255, 255, 0.3);
  border-radius: 4px;
  overflow: hidden;
  margin-bottom: 10px;
}

.progress-bar {
  height: 100%;
  background: linear-gradient(90deg, #00ff88, #00ccff);
  transition: width 0.3s ease;
  border-radius: 4px;
}

.counter-hint {
  font-size: 0.9rem;
  opacity: 0.8;
  font-style: italic;
}

.control-buttons {
  grid-column: 1 / -1;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 15px;
  margin-bottom: 20px;
}

.btn {
  padding: 15px 20px;
  border: none;
  border-radius: 10px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  text-align: center;
}

.increment-btn {
  background: linear-gradient(135deg, #4CAF50, #45a049);
  color: white;
}

.increment-btn:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(76, 175, 80, 0.3);
}

.decrement-btn {
  background: linear-gradient(135deg, #f44336, #da190b);
  color: white;
}

.decrement-btn:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(244, 67, 54, 0.3);
}

.reset-btn {
  background: linear-gradient(135deg, #ff9800, #f57c00);
  color: white;
}

.reset-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(255, 152, 0, 0.3);
}

.btn:disabled {
  background: #bdc3c7;
  cursor: not-allowed;
  transform: none;
  box-shadow: none;
}

.keyboard-hints {
  background: white;
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  border: 1px solid #e1e5e9;
}

.keyboard-hints h4 {
  color: #2c3e50;
  margin-bottom: 15px;
  text-align: center;
}

.hint-grid {
  display: grid;
  gap: 10px;
}

.hint-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;
  background: #f8f9fa;
  border-radius: 8px;
}

kbd {
  background: #2c3e50;
  color: white;
  padding: 5px 10px;
  border-radius: 5px;
  font-family: monospace;
  font-weight: bold;
}

.target-form {
  background: white;
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  border: 1px solid #e1e5e9;
}

.target-form h4 {
  color: #2c3e50;
  margin-bottom: 15px;
  text-align: center;
}

.form-inline {
  display: flex;
  gap: 10px;
}

.target-input {
  flex: 1;
  padding: 10px;
  border: 2px solid #e1e5e9;
  border-radius: 8px;
  font-size: 14px;
}

.target-input:focus {
  outline: none;
  border-color: #3498db;
}

.submit-btn {
  background: linear-gradient(135deg, #3498db, #2980b9);
  color: white;
  padding: 10px 20px;
  border-radius: 8px;
}

.submit-btn:hover {
  transform: translateY(-1px);
  box-shadow: 0 3px 10px rgba(52, 152, 219, 0.3);
}

.stats-panel {
  grid-column: 1 / -1;
  background: white;
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  border: 1px solid #e1e5e9;
}

.stats-panel h4 {
  color: #2c3e50;
  margin-bottom: 15px;
  text-align: center;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  gap: 15px;
}

.stat-item {
  text-align: center;
  padding: 15px;
  background: #f8f9fa;
  border-radius: 10px;
  border-left: 4px solid #3498db;
}

.stat-value {
  font-size: 2rem;
  font-weight: bold;
  color: #2c3e50;
  margin-bottom: 5px;
}

.stat-label {
  font-size: 0.9rem;
  color: #7f8c8d;
}

.history-panel {
  grid-column: 1 / -1;
  background: white;
  padding: 20px;
  border-radius: 15px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
  border: 1px solid #e1e5e9;
}

.history-panel h4 {
  color: #2c3e50;
  margin-bottom: 15px;
  text-align: center;
}

.history-list {
  max-height: 300px;
  overflow-y: auto;
}

.history-item {
  display: flex;
  align-items: center;
  padding: 10px;
  margin-bottom: 8px;
  background: #f8f9fa;
  border-radius: 8px;
  border-left: 4px solid #3498db;
  transition: all 0.3s ease;
}

.history-item:hover {
  background: #e9ecef;
  transform: translateX(5px);
}

.action-increment {
  border-left-color: #4CAF50;
}

.action-decrement {
  border-left-color: #f44336;
}

.action-reset {
  border-left-color: #ff9800;
}

.action-double-click {
  border-left-color: #9c27b0;
}

.action-set-target {
  border-left-color: #2196F3;
}

.action-icon {
  margin-right: 10px;
  font-size: 1.2rem;
}

.action-text {
  flex: 1;
  font-weight: 500;
  color: #2c3e50;
}

.action-time {
  font-size: 0.9rem;
  color: #7f8c8d;
  font-family: monospace;
}

.no-history {
  text-align: center;
  color: #7f8c8d;
  font-style: italic;
  padding: 20px;
}

@media (max-width: 768px) {
  .counter-container {
    grid-template-columns: 1fr;
  }

  .control-buttons {
    grid-template-columns: 1fr;
  }

  .stats-grid {
    grid-template-columns: repeat(2, 1fr);
  }

  .form-inline {
    flex-direction: column;
  }

  .counter-value {
    font-size: 3rem;
  }
}
</style>
