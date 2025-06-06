<template>
  <div class="answering-area">
    <h2>🎯 參考答案 - Event 事件處理</h2>
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
          <p v-if="searchResults.length === 0 && searchText">沒有找到相關結果</p>
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
const playerX = ref(50)
const playerY = ref(50)

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
const searchData = ref([
  { id: 1, name: 'Apple 蘋果' },
  { id: 2, name: 'Banana 香蕉' },
  { id: 3, name: 'Cherry 櫻桃' },
  { id: 4, name: 'Date 椰棗' },
  { id: 5, name: 'Elderberry 接骨木果' }
])

// 點擊處理
const handleClick = () => {
  clickCount.value++
  comboCount.value++

  // 重置連擊計時器
  if (comboInterval.value) {
    clearInterval(comboInterval.value)
  }

  comboTimer.value = 3
  comboInterval.value = setInterval(() => {
    comboTimer.value--
    if (comboTimer.value <= 0) {
      // 更新最高連擊記錄
      if (comboCount.value > maxCombo.value) {
        maxCombo.value = comboCount.value
      }
      comboCount.value = 0
      clearInterval(comboInterval.value)
      comboInterval.value = null
    }
  }, 1000)

  addEventLog('單擊')
}

// 雙擊處理
const handleDoubleClick = () => {
  clickCount.value += 5 // 雙擊獲得額外分數
  addEventLog('雙擊 (+5 分)')
}

// 重置計數器
const resetCounter = () => {
  clickCount.value = 0
  comboCount.value = 0
  maxCombo.value = 0
  comboTimer.value = 0

  if (comboInterval.value) {
    clearInterval(comboInterval.value)
    comboInterval.value = null
  }

  addEventLog('重置計數器')
}

// 按鍵按下處理
const handleKeyDown = (event) => {
  if (!gameAreaFocused.value) return

  event.preventDefault()
  pressedKeys.value.add(event.code)

  const moveSpeed = 10
  const gameAreaWidth = 600 // 假設遊戲區域寬度
  const gameAreaHeight = 400 // 假設遊戲區域高度

  // 處理移動
  switch (event.code) {
    case 'KeyW':
    case 'ArrowUp':
      playerY.value = Math.max(0, playerY.value - moveSpeed)
      break
    case 'KeyS':
    case 'ArrowDown':
      playerY.value = Math.min(gameAreaHeight - 50, playerY.value + moveSpeed)
      break
    case 'KeyA':
    case 'ArrowLeft':
      playerX.value = Math.max(0, playerX.value - moveSpeed)
      break
    case 'KeyD':
    case 'ArrowRight':
      playerX.value = Math.min(gameAreaWidth - 50, playerX.value + moveSpeed)
      break
    case 'Space':
      // 發射功能
      addEventLog('發射！')
      gameScore.value += 10
      break
  }

  // 更新玩家位置
  playerPosition.value = {
    transform: `translate(${playerX.value}px, ${playerY.value}px)`
  }

  addEventLog(`按下 ${event.key}`)
}

// 按鍵放開處理
const handleKeyUp = (event) => {
  pressedKeys.value.delete(event.code)
  addEventLog(`放開 ${event.key}`)
}

// 滑鼠移動處理
const handleMouseMove = (event) => {
  const rect = event.currentTarget.getBoundingClientRect()
  const x = event.clientX - rect.left
  const y = event.clientY - rect.top

  mousePosition.value = { x, y }

  // 添加滑鼠軌跡
  mouseTrail.value.push({
    x: x - 10,
    y: y - 10,
    opacity: 1
  })

  // 限制軌跡數量
  if (mouseTrail.value.length > 20) {
    mouseTrail.value.shift()
  }

  // 更新軌跡透明度
  mouseTrail.value.forEach((trail, index) => {
    trail.opacity = (index + 1) / mouseTrail.value.length
  })
}

// 滑鼠進入區域
const handleMouseEnter = () => {
  isMouseInArea.value = true
  addEventLog('滑鼠進入區域')
}

// 滑鼠離開區域
const handleMouseLeave = () => {
  isMouseInArea.value = false
  mouseTrail.value = []
  addEventLog('滑鼠離開區域')
}

// 右鍵點擊處理
const handleRightClick = () => {
  rightClickCount.value++
  addEventLog('右鍵點擊')
}

// 輸入處理（即時搜尋）
const handleInput = () => {
  const query = searchText.value.toLowerCase().trim()

  if (query) {
    searchResults.value = searchData.value.filter(item =>
      item.name.toLowerCase().includes(query)
    )
  } else {
    searchResults.value = []
  }

  addEventLog(`搜尋: "${searchText.value}"`)
}

// 焦點獲得
const handleFocus = () => {
  addEventLog('輸入框獲得焦點')
}

// 焦點失去
const handleBlur = () => {
  addEventLog('輸入框失去焦點')
}

// Enter 鍵處理
const handleEnterKey = () => {
  if (searchText.value.trim()) {
    addEventLog(`執行搜尋: "${searchText.value}"`)
    // 可以在這裡執行特殊的搜尋邏輯
  }
}

// Escape 鍵處理
const handleEscapeKey = () => {
  searchText.value = ''
  searchResults.value = []
  addEventLog('清空搜尋 (ESC)')
}

// 新增事件日誌
const addEventLog = (eventType) => {
  const now = new Date()
  const time = now.toLocaleTimeString()

  eventLogs.value.unshift({
    time,
    event: eventType
  })

  // 限制日誌數量
  if (eventLogs.value.length > 50) {
    eventLogs.value.pop()
  }
}

// 清空事件日誌
const clearEventLogs = () => {
  eventLogs.value = []
  addEventLog('清空事件日誌')
}

// 生成遊戲道具
const generateGameItems = () => {
  if (gameItems.value.length < 5) {
    const item = {
      x: Math.random() * 550, // 避免超出邊界
      y: -50,
      type: Math.random() > 0.3 ? 'coin' : 'bomb'
    }
    gameItems.value.push(item)
  }
}

// 更新遊戲道具位置
const updateGameItems = () => {
  gameItems.value.forEach((item, index) => {
    item.y += 2

    // 檢查碰撞
    const playerCenterX = playerX.value + 25
    const playerCenterY = playerY.value + 25
    const itemCenterX = item.x + 25
    const itemCenterY = item.y + 25

    const distance = Math.sqrt(
      Math.pow(playerCenterX - itemCenterX, 2) +
      Math.pow(playerCenterY - itemCenterY, 2)
    )

    if (distance < 40) {
      // 發生碰撞
      if (item.type === 'coin') {
        gameScore.value += 50
        addEventLog('獲得金幣 (+50)')
      } else {
        playerLife.value--
        addEventLog('碰到炸彈 (-1 生命)')
        if (playerLife.value <= 0) {
          addEventLog('遊戲結束！')
          // 重置遊戲
          playerLife.value = 3
          gameScore.value = 0
          gameItems.value = []
        }
      }
      gameItems.value.splice(index, 1)
    }

    // 移除超出邊界的道具
    if (item.y > 450) {
      gameItems.value.splice(index, 1)
    }
  })
}

// 遊戲循環
let gameLoop = null

// 生命週期
onMounted(() => {
  addEventLog('遊戲初始化完成')

  // 啟動遊戲循環
  gameLoop = setInterval(() => {
    generateGameItems()
    updateGameItems()
  }, 100)
})

onBeforeUnmount(() => {
  // 清理計時器
  if (comboInterval.value) {
    clearInterval(comboInterval.value)
  }

  if (gameLoop) {
    clearInterval(gameLoop)
  }

  addEventLog('組件即將銷毀')
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

.game-area:focus {
  box-shadow: 0 0 0 3px rgba(232, 62, 140, 0.3);
}

.player {
  position: absolute;
  font-size: 2rem;
  transition: transform 0.1s ease;
  z-index: 5;
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
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
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

.key:nth-child(5) {
  grid-column: 1 / -1;
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
  transform: scale(0.95);
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
  transition: transform 0.1s ease;
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
  transition: border-color 0.3s ease;
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
  transition: background-color 0.2s ease;
}

.search-results li:hover {
  background-color: #f8f9fa;
}

.search-results li:last-child {
  border-bottom: none;
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
  background: #f8f9fa;
}

.log-entry {
  display: flex;
  gap: 1rem;
  padding: 0.25rem 0;
  border-bottom: 1px solid #f1f3f4;
  font-family: monospace;
  font-size: 0.9rem;
}

.log-entry:last-child {
  border-bottom: none;
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
  transition: all 0.3s ease;
}

.btn:hover {
  transform: translateY(-1px);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.btn-primary {
  background: #007bff;
  color: white;
}

.btn-primary:hover {
  background: #0056b3;
}

.btn-secondary {
  background: #6c757d;
  color: white;
}

.btn-secondary:hover {
  background: #545b62;
}

.btn-danger {
  background: #dc3545;
  color: white;
}

.btn-danger:hover {
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

  .key-display {
    grid-template-columns: repeat(2, 1fr);
  }
}
</style>
