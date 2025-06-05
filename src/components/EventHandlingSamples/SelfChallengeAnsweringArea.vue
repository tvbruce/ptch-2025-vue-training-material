<template>
  <div class="answering-area">
    <h2>🎯 實作練習區 - Event 事件處理</h2>
    <p class="description">
      📝 <strong>任務：</strong>建立一個互動遊戲應用，實作各種事件處理功能
    </p>

    <!-- 任務一：點擊計數器 -->
    <div class="task-section">
      <h3>🖱️ 任務一：點擊計數器</h3>
      <div class="counter-container">
        <div class="counter-display">
          <h4>點擊次數：{{ clickCount }}</h4>
          <p>連擊數：{{ comboCount }}</p>
          <p>最高連擊：{{ maxCombo }}</p>
        </div>

        <div class="counter-controls">
          <button @click="handleClick" class="btn btn-primary">點我！</button>
          <button @dblclick="handleDoubleClick" class="btn btn-secondary">雙擊我！</button>
          <button @click="resetCounter" class="btn btn-danger">重置</button>
        </div>

        <div class="combo-timer">
          <p>連擊剩餘時間：{{ comboTimer }}s</p>
          <div class="timer-bar">
            <div class="timer-fill" :style="{ width: (comboTimer / 3) * 100 + '%' }"></div>
          </div>
        </div>
      </div>
    </div>

    <!-- 任務二：鍵盤操作 -->
    <div class="task-section">
      <h3>⌨️ 任務二：鍵盤操作</h3>
      <div class="keyboard-container">
        <div class="game-area" tabindex="0" @keydown="handleKeyDown" @keyup="handleKeyUp"
          @focus="gameAreaFocused = true" @blur="gameAreaFocused = false">

          <div class="player" :style="playerPosition">🚀</div>

          <div v-for="(item, index) in gameItems" :key="index" class="game-item"
            :style="{ left: item.x + 'px', top: item.y + 'px' }">
            {{ item.type === 'coin' ? '🪙' : '💣' }}
          </div>

          <div class="game-info">
            <p>使用 WASD 或方向鍵移動</p>
            <p>空格鍵：發射</p>
            <p>分數：{{ gameScore }}</p>
            <p>生命：{{ playerLife }}</p>
          </div>
        </div>

        <div class="key-status">
          <h4>按鍵狀態：</h4>
          <div class="key-display">
            <div class="key" :class="{ active: pressedKeys.has('KeyW') }">W</div>
            <div class="key" :class="{ active: pressedKeys.has('KeyA') }">A</div>
            <div class="key" :class="{ active: pressedKeys.has('KeyS') }">S</div>
            <div class="key" :class="{ active: pressedKeys.has('KeyD') }">D</div>
            <div class="key" :class="{ active: pressedKeys.has('Space') }">空格</div>
          </div>
        </div>
      </div>
    </div>

    <!-- 任務三：滑鼠追蹤 -->
    <div class="task-section">
      <h3>🖱️ 任務三：滑鼠追蹤</h3>
      <div class="mouse-container">
        <div class="mouse-area" @mousemove="handleMouseMove" @mouseenter="handleMouseEnter"
          @mouseleave="handleMouseLeave" @contextmenu.prevent="handleRightClick">

          <div class="mouse-cursor" :style="{ left: mousePosition.x + 'px', top: mousePosition.y + 'px' }">
            🎯
          </div>

          <div v-for="(trail, index) in mouseTrail" :key="index" class="mouse-trail" :style="{
            left: trail.x + 'px',
            top: trail.y + 'px',
            opacity: trail.opacity
          }">
            ⭐
          </div>

          <div class="mouse-info">
            <p>滑鼠位置：{{ mousePosition.x }}, {{ mousePosition.y }}</p>
            <p>在區域內：{{ isMouseInArea ? '是' : '否' }}</p>
            <p>右鍵點擊次數：{{ rightClickCount }}</p>
          </div>
        </div>
      </div>
    </div>

    <!-- 任務四：表單事件 -->
    <div class="task-section">
      <h3>📋 任務四：表單事件處理</h3>
      <div class="form-container">
        <div class="form-group">
          <label>即時搜尋：</label>
          <input v-model="searchText" @input="handleInput" @focus="handleFocus" @blur="handleBlur"
            @keydown.enter="handleEnterKey" @keydown.esc="handleEscapeKey" placeholder="輸入搜尋內容..." class="form-input">
          <p>輸入長度：{{ searchText.length }}</p>
        </div>

        <div class="search-results">
          <h4>搜尋結果：</h4>
          <ul>
            <li v-for="result in searchResults" :key="result.id">
              {{ result.name }}
            </li>
          </ul>
        </div>

        <div class="event-log">
          <h4>事件日誌：</h4>
          <div class="log-container">
            <div v-for="(log, index) in eventLogs" :key="index" class="log-entry">
              <span class="log-time">{{ log.time }}</span>
              <span class="log-event">{{ log.event }}</span>
            </div>
          </div>
          <button @click="clearEventLogs" class="btn btn-secondary">清空日誌</button>
        </div>
      </div>
    </div>

    <!-- 開發提示 -->
    <div class="hint-section">
      <h4>💡 開發提示</h4>
      <ul>
        <li>@click, @dblclick: 處理滑鼠點擊事件</li>
        <li>@keydown, @keyup: 處理鍵盤事件</li>
        <li>@mousemove, @mouseenter, @mouseleave: 處理滑鼠移動事件</li>
        <li>事件修飾符：.prevent, .stop, .once, .passive</li>
        <li>按鍵修飾符：.enter, .tab, .delete, .esc, .space, .up, .down, .left, .right</li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

// 點擊計數器狀態
const clickCount = ref(0)
const comboCount = ref(0)
const maxCombo = ref(0)
const comboTimer = ref(0)
const comboInterval = ref(null)

// 鍵盤遊戲狀態
const gameAreaFocused = ref(false)
const pressedKeys = ref(new Set())
const playerPosition = ref({ transform: 'translate(50px, 50px)' })
const gameItems = ref([])
const gameScore = ref(0)
const playerLife = ref(3)

// 滑鼠追蹤狀態
const mousePosition = ref({ x: 0, y: 0 })
const mouseTrail = ref([])
const isMouseInArea = ref(false)
const rightClickCount = ref(0)

// 表單事件狀態
const searchText = ref('')
const searchResults = ref([])
const eventLogs = ref([])

// 模擬搜尋資料
// eslint-disable-next-line no-unused-vars
const searchData = ref([
  { id: 1, name: 'Apple 蘋果' },
  { id: 2, name: 'Banana 香蕉' },
  { id: 3, name: 'Cherry 櫻桃' },
  { id: 4, name: 'Date 椰棗' },
  { id: 5, name: 'Elderberry 接骨木果' }
])

// 🎯 任務：實作 handleClick 方法

const handleClick = () => {
  // 請在這裡實作點擊處理邏輯
  // 1. 增加點擊次數
  // 2. 處理連擊邏輯
  // 3. 重置連擊計時器
  console.log('請實作點擊處理功能')
}

// 🎯 任務：實作 handleDoubleClick 方法

const handleDoubleClick = () => {
  // 請在這裡實作雙擊處理邏輯
  // 雙擊可以獲得額外分數
  console.log('請實作雙擊處理功能')
}

// 🎯 任務：實作 resetCounter 方法
const resetCounter = () => {
  // 請在這裡實作重置計數器邏輯
  console.log('請實作重置計數器功能')
}

// 🎯 任務：實作 handleKeyDown 方法
// eslint-disable-next-line no-unused-vars
const handleKeyDown = (event) => {
  // 請在這裡實作按鍵按下處理邏輯
  // 1. 記錄按下的按鍵
  // 2. 處理玩家移動
  // 3. 處理發射等特殊功能
  console.log('請實作按鍵按下處理功能')
}

// 🎯 任務：實作 handleKeyUp 方法
// eslint-disable-next-line no-unused-vars
const handleKeyUp = (event) => {
  // 請在這裡實作按鍵放開處理邏輯
  // 移除按鍵狀態
  console.log('請實作按鍵放開處理功能')
}

// 🎯 任務：實作 handleMouseMove 方法
// eslint-disable-next-line no-unused-vars
const handleMouseMove = (event) => {
  // 請在這裡實作滑鼠移動處理邏輯
  // 1. 更新滑鼠位置
  // 2. 更新滑鼠軌跡
  console.log('請實作滑鼠移動處理功能')
}

// 🎯 任務：實作 handleMouseEnter 方法
const handleMouseEnter = () => {
  // 請在這裡實作滑鼠進入區域處理邏輯
  console.log('請實作滑鼠進入處理功能')
}

// 🎯 任務：實作 handleMouseLeave 方法
const handleMouseLeave = () => {
  // 請在這裡實作滑鼠離開區域處理邏輯
  console.log('請實作滑鼠離開處理功能')
}

// 🎯 任務：實作 handleRightClick 方法
const handleRightClick = () => {
  // 請在這裡實作右鍵點擊處理邏輯
  console.log('請實作右鍵點擊處理功能')
}

// 🎯 任務：實作 handleInput 方法
const handleInput = () => {
  // 請在這裡實作輸入處理邏輯
  // 即時搜尋功能
  console.log('請實作輸入處理功能')
}

// 🎯 任務：實作 handleFocus 方法
const handleFocus = () => {
  // 請在這裡實作焦點獲得處理邏輯
  console.log('請實作焦點處理功能')
}

// 🎯 任務：實作 handleBlur 方法
const handleBlur = () => {
  // 請在這裡實作焦點失去處理邏輯
  console.log('請實作失焦處理功能')
}

// 🎯 任務：實作 handleEnterKey 方法
const handleEnterKey = () => {
  // 請在這裡實作Enter鍵處理邏輯
  console.log('請實作Enter鍵處理功能')
}

// 🎯 任務：實作 handleEscapeKey 方法
const handleEscapeKey = () => {
  // 請在這裡實作Escape鍵處理邏輯
  console.log('請實作Escape鍵處理功能')
}

// 🎯 任務：實作 addEventLog 方法
// eslint-disable-next-line no-unused-vars
const addEventLog = (eventType) => {
  // 請在這裡實作新增事件日誌邏輯
  console.log('請實作事件日誌功能')
}

// 🎯 任務：實作 clearEventLogs 方法
const clearEventLogs = () => {
  // 請在這裡實作清空事件日誌邏輯
  console.log('請實作清空日誌功能')
}

// 生命週期
onMounted(() => {
  // 初始化遊戲
  console.log('組件已掛載')
})

onBeforeUnmount(() => {
  // 清理計時器
  if (comboInterval.value) {
    clearInterval(comboInterval.value)
  }
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
  border-left: 4px solid #e83e8c;
}

.counter-container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 2rem;
  align-items: start;
}

.counter-display {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  text-align: center;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.counter-controls {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.combo-timer {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.timer-bar {
  width: 100%;
  height: 10px;
  background: #e9ecef;
  border-radius: 5px;
  overflow: hidden;
  margin-top: 0.5rem;
}

.timer-fill {
  height: 100%;
  background: #28a745;
  transition: width 0.1s ease;
}

.keyboard-container {
  display: grid;
  grid-template-columns: 3fr 1fr;
  gap: 2rem;
}

.game-area {
  position: relative;
  width: 100%;
  height: 400px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 8px;
  overflow: hidden;
  outline: none;
  cursor: none;
}

.player {
  position: absolute;
  font-size: 2rem;
  transition: transform 0.1s ease;
}

.game-item {
  position: absolute;
  font-size: 1.5rem;
  animation: fall 3s linear infinite;
}

.game-info {
  position: absolute;
  top: 10px;
  left: 10px;
  color: white;
  font-size: 0.9rem;
}

.key-status {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.key-display {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 0.5rem;
  margin-top: 1rem;
}

.key {
  padding: 0.5rem;
  background: #f8f9fa;
  border: 2px solid #dee2e6;
  border-radius: 4px;
  text-align: center;
  font-weight: bold;
  transition: all 0.1s ease;
}

.key.active {
  background: #007bff;
  color: white;
  border-color: #0056b3;
}

.mouse-container {
  background: white;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.mouse-area {
  position: relative;
  width: 100%;
  height: 300px;
  background: linear-gradient(45deg, #ff9a9e 0%, #fecfef 100%);
  border-radius: 8px;
  overflow: hidden;
  cursor: none;
}

.mouse-cursor {
  position: absolute;
  font-size: 1.5rem;
  pointer-events: none;
  z-index: 10;
}

.mouse-trail {
  position: absolute;
  font-size: 1rem;
  pointer-events: none;
  animation: fade-out 1s ease-out forwards;
}

.mouse-info {
  position: absolute;
  top: 10px;
  left: 10px;
  color: white;
  font-size: 0.9rem;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
}

.form-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2rem;
}

.form-group {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.form-input {
  width: 100%;
  padding: 0.75rem;
  border: 2px solid #dee2e6;
  border-radius: 4px;
  font-size: 1rem;
  margin-top: 0.5rem;
}

.form-input:focus {
  outline: none;
  border-color: #e83e8c;
}

.search-results {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  grid-column: 1 / -1;
}

.search-results ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.search-results li {
  padding: 0.5rem;
  border-bottom: 1px solid #f1f3f4;
}

.event-log {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  grid-column: 1 / -1;
}

.log-container {
  max-height: 200px;
  overflow-y: auto;
  border: 1px solid #e9ecef;
  border-radius: 4px;
  padding: 1rem;
  margin: 1rem 0;
}

.log-entry {
  display: flex;
  gap: 1rem;
  padding: 0.25rem 0;
  border-bottom: 1px solid #f1f3f4;
  font-family: monospace;
  font-size: 0.9rem;
}

.log-time {
  color: #6c757d;
  min-width: 80px;
}

.log-event {
  color: #495057;
}

.btn {
  padding: 0.75rem 1.5rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
  transition: background-color 0.3s ease;
}

.btn-primary {
  background: #007bff;
  color: white;
}

.btn-secondary {
  background: #6c757d;
  color: white;
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

@keyframes fall {
  from {
    transform: translateY(-50px);
  }

  to {
    transform: translateY(450px);
  }
}

@keyframes fade-out {
  from {
    opacity: 1;
    transform: scale(1);
  }

  to {
    opacity: 0;
    transform: scale(0.5);
  }
}

@media (max-width: 768px) {

  .counter-container,
  .keyboard-container,
  .form-container {
    grid-template-columns: 1fr;
  }
}
</style>
