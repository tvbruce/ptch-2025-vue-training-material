<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - Event 事件處理</h2>
    <p class="route-info">📍 路徑：/EventHandlingSamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>挑戰任務：</strong>建立一個簡單的互動計數器，練習各種事件處理技巧
    </p>

    <!-- 練習規格說明區域 -->
    <div class="practice-specs">
      <h3>📋 練習規格說明</h3>
      <div class="specs-container">
        <div class="spec-item">
          <h4>🎯 練習目標</h4>
          <p>透過實作一個簡單的互動計數器，學習 Vue.js 中各種事件處理方式</p>
        </div>

        <div class="spec-item">
          <h4>📚 需要完成的任務</h4>
          <div class="task-grid">
            <div class="task-card">
              <h5>任務 1：基本點擊事件</h5>
              <ul>
                <li>實作「增加」按鈕的點擊事件</li>
                <li>實作「減少」按鈕的點擊事件</li>
                <li>實作「重置」按鈕的點擊事件</li>
              </ul>
              <div class="hint">
                💡 <strong>提示：</strong>使用 @click 事件綁定函數
              </div>
            </div>

            <div class="task-card">
              <h5>任務 2：鍵盤事件處理</h5>
              <ul>
                <li>按下 <kbd>Space</kbd> 鍵增加計數</li>
                <li>按下 <kbd>r</kbd> 或 <kbd>R</kbd> 鍵重置計數</li>
                <li>按下 <kbd>-</kbd> 鍵減少計數</li>
              </ul>
              <div class="hint">
                💡 <strong>提示：</strong>使用全域 keydown 事件監聽器
              </div>
            </div>

            <div class="task-card">
              <h5>任務 3：滑鼠事件處理</h5>
              <ul>
                <li>滑鼠進入計數顯示區域時變色</li>
                <li>滑鼠離開時恢復原色</li>
                <li>追蹤滑鼠在區域內的位置</li>
              </ul>
              <div class="hint">
                💡 <strong>提示：</strong>使用 @mouseenter、@mouseleave、@mousemove
              </div>
            </div>

            <div class="task-card">
              <h5>任務 4：事件修飾符</h5>
              <ul>
                <li>表單提交時阻止頁面刷新</li>
                <li>雙擊時阻止文字選取</li>
                <li>右鍵選單時顯示自訂選單</li>
              </ul>
              <div class="hint">
                💡 <strong>提示：</strong>使用 .prevent、.stop 等修飾符
              </div>
            </div>
          </div>
        </div>

        <div class="spec-item">
          <h4>⚙️ 實作邏輯說明</h4>
          <div class="logic-explanation">
            <div class="logic-item">
              <h6>計數器邏輯：</h6>
              <ul>
                <li>初始值為 0</li>
                <li>增加：每次 +1，最大值 100</li>
                <li>減少：每次 -1，最小值 0</li>
                <li>重置：回到 0</li>
              </ul>
            </div>
            <div class="logic-item">
              <h6>視覺回饋邏輯：</h6>
              <ul>
                <li>計數 > 50 時顯示綠色</li>
                <li>計數 > 80 時顯示金色</li>
                <li>滑鼠懸停時背景變亮</li>
                <li>按鍵時顯示動畫效果</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- 實作區域 -->
    <div class="demo-section">
      <h3>🎮 互動計數器 - 實作區域</h3>

      <!-- 計數顯示區域 -->
      <div class="counter-display" :class="getCounterClass()" @mouseenter="handleMouseEnter"
        @mouseleave="handleMouseLeave" @mousemove="handleMouseMove">
        <div class="counter-value">{{ count }}</div>
        <div class="counter-label">目前計數</div>
        <div v-if="isMouseInside" class="mouse-position">
          滑鼠位置：{{ mousePos.x }}, {{ mousePos.y }}
        </div>
      </div>

      <!-- 按鈕控制區域 -->
      <div class="button-controls">
        <!-- TODO: 學員需要完成這些按鈕的事件處理 -->
        <button class="btn btn-increase" @click="increaseCount">
          ➕ 增加 (+1)
        </button>
        <button class="btn btn-decrease" @click="decreaseCount">
          ➖ 減少 (-1)
        </button>
        <button class="btn btn-reset" @click="resetCount">
          🔄 重置 (0)
        </button>
      </div>

      <!-- 表單測試區域 -->
      <div class="form-section">
        <h4>📝 表單事件測試</h4>
        <!-- TODO: 學員需要完成表單提交的事件處理 -->
        <form @submit.prevent="handleFormSubmit" class="counter-form">
          <label for="step-input">設定步進值：</label>
          <input type="number" id="step-input" v-model="stepValue" min="1" max="10" @keyup.enter="handleFormSubmit">
          <button type="submit">套用</button>
        </form>
        <p>目前步進值：{{ stepValue }}</p>
      </div>

      <!-- 右鍵選單測試區域 -->
      <div class="context-menu-area" @contextmenu.prevent="handleContextMenu">
        <p>在這個區域按右鍵測試自訂選單</p>
        <!-- TODO: 學員需要完成右鍵選單的顯示/隱藏 -->
        <div v-if="showContextMenu" class="context-menu"
          :style="{ left: contextMenuPos.x + 'px', top: contextMenuPos.y + 'px' }">
          <div class="menu-item" @click="handleMenuAction('increase')">快速增加 +10</div>
          <div class="menu-item" @click="handleMenuAction('decrease')">快速減少 -10</div>
          <div class="menu-item" @click="handleMenuAction('reset')">重置計數</div>
        </div>
      </div>
    </div>

    <!-- 狀態顯示區域 -->
    <div class="status-section">
      <h4>📊 事件狀態監控</h4>
      <div class="status-grid">
        <div class="status-item">
          <label>總點擊次數：</label>
          <span>{{ totalClicks }}</span>
        </div>
        <div class="status-item">
          <label>上次按鍵：</label>
          <span>{{ lastKey || '無' }}</span>
        </div>
        <div class="status-item">
          <label>滑鼠狀態：</label>
          <span>{{ mouseStatus }}</span>
        </div>
        <div class="status-item">
          <label>計數顏色：</label>
          <span>{{ getCounterColorName() }}</span>
        </div>
      </div>
    </div>

    <!-- 實作提示區域 -->
    <div class="hint-section">
      <h4>💡 實作提示與參考代碼</h4>
      <details>
        <summary>點擊查看實作提示</summary>
        <div class="code-examples">
          <h5>1. 基本點擊事件實作：</h5>
          <pre v-pre><code>// 增加計數函數
const increaseCount = () => {
  if (count.value < 100) {
    count.value += stepValue.value
    totalClicks.value++
  }
}</code></pre>

          <h5>2. 鍵盤事件實作：</h5>
          <pre v-pre><code>const handleKeydown = (event) => {
  switch(event.key) {
    case ' ':
      event.preventDefault()
      increaseCount()
      break
    case 'r':
    case 'R':
      resetCount()
      break
  }
  lastKey.value = event.key
}</code></pre>

          <h5>3. 滑鼠事件實作：</h5>
          <pre v-pre><code>const handleMouseEnter = () => {
  isMouseInside.value = true
  mouseStatus.value = '進入'
}

const handleMouseMove = (event) => {
  mousePos.value = {
    x: event.offsetX,
    y: event.offsetY
  }
}</code></pre>

          <h5>4. 事件修飾符實作：</h5>
          <pre v-pre><code>// 阻止表單預設提交行為
&lt;form @submit.prevent="handleSubmit"&gt;

// 阻止右鍵選單
&lt;div @contextmenu.prevent="showCustomMenu"&gt;</code></pre>
        </div>
      </details>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// 計數器狀態
const count = ref(0)
const stepValue = ref(1)
const totalClicks = ref(0)

// 滑鼠相關狀態
const isMouseInside = ref(false)
const mousePos = ref({ x: 0, y: 0 })
const mouseStatus = ref('靜止')

// 鍵盤相關狀態
const lastKey = ref('')

// 右鍵選單狀態
const showContextMenu = ref(false)
const contextMenuPos = ref({ x: 0, y: 0 })

// TODO: 學員需要完成以下函數實作

// 1. 增加計數 (按鈕點擊和空白鍵)
const increaseCount = () => {
  // TODO: 請在這裡實作增加計數的邏輯
  // 提示：檢查 count.value < 100，然後 count.value += stepValue.value
  // 別忘了更新 totalClicks.value++
}

// 2. 減少計數 (按鈕點擊和減號鍵)
const decreaseCount = () => {
  // TODO: 請在這裡實作減少計數的邏輯
  // 提示：檢查 count.value > 0，然後 count.value -= stepValue.value
  // 別忘了更新 totalClicks.value++
}

// 3. 重置計數 (按鈕點擊和R鍵)
const resetCount = () => {
  // TODO: 請在這裡實作重置計數的邏輯
  // 提示：設定 count.value = 0
  // 別忘了更新 totalClicks.value++
}

// 4. 滑鼠進入事件
const handleMouseEnter = () => {
  // TODO: 請在這裡實作滑鼠進入的邏輯
  // 提示：設定 isMouseInside.value = true
  // 提示：設定 mouseStatus.value = '進入'
}

// 5. 滑鼠離開事件
const handleMouseLeave = () => {
  // TODO: 請在這裡實作滑鼠離開的邏輯
  // 提示：設定 isMouseInside.value = false
  // 提示：設定 mouseStatus.value = '離開'
  // 提示：隱藏右鍵選單 showContextMenu.value = false
}

// 6. 滑鼠移動事件
const handleMouseMove = (event) => { // eslint-disable-line no-unused-vars
  // TODO: 請在這裡實作滑鼠移動的邏輯
  // 提示：更新 mousePos.value = { x: event.offsetX, y: event.offsetY }
  // 提示：設定 mouseStatus.value = '移動中'
}

// 7. 鍵盤按下事件
const handleKeydown = (event) => { // eslint-disable-line no-unused-vars
  // TODO: 請在這裡實作鍵盤事件的邏輯
  // 提示：使用 switch(event.key) 判斷按鍵
  // 提示：' ' (空白鍵) - 呼叫 increaseCount()，記得 event.preventDefault()
  // 提示：'r' 或 'R' - 呼叫 resetCount()
  // 提示：'-' (減號鍵) - 呼叫 decreaseCount()
  // 提示：設定 lastKey.value = event.key
}

// 8. 表單提交事件
const handleFormSubmit = () => {
  // TODO: 請在這裡實作表單提交的邏輯
  // 提示：檢查 stepValue.value 是否在 1-10 範圍內
  // 提示：如果不在範圍內，使用 alert() 顯示錯誤訊息並 return
  // 提示：如果正確，顯示成功訊息
}

// 9. 右鍵選單事件
const handleContextMenu = (event) => { // eslint-disable-line no-unused-vars
  // TODO: 請在這裡實作右鍵選單的邏輯
  // 提示：使用 event.preventDefault() 阻止預設右鍵選單
  // 提示：設定 showContextMenu.value = true
  // 提示：設定選單位置 contextMenuPos.value = { x: event.clientX, y: event.clientY }
}

// 10. 選單項目點擊
const handleMenuAction = (action) => { // eslint-disable-line no-unused-vars
  // TODO: 請在這裡實作選單動作的邏輯
  // 提示：使用 switch(action) 判斷動作類型
  // 提示：'increase' - 快速增加 10，呼叫 increaseCount() 多次或直接加 10
  // 提示：'decrease' - 快速減少 10，呼叫 decreaseCount() 多次或直接減 10
  // 提示：'reset' - 呼叫 resetCount()
  // 提示：最後設定 showContextMenu.value = false 隱藏選單
}

// 輔助函數
const getCounterClass = () => {
  return {
    'counter-normal': count.value <= 50,
    'counter-good': count.value > 50 && count.value <= 80,
    'counter-excellent': count.value > 80,
    'mouse-inside': isMouseInside.value
  }
}

const getCounterColorName = () => {
  if (count.value <= 50) return '藍色 (正常)'
  if (count.value <= 80) return '綠色 (良好)'
  return '金色 (優秀)'
}

// 生命週期
onMounted(() => {
  // TODO: 學員需要在這裡添加全域事件監聽器
  // 提示：document.addEventListener('keydown', handleKeydown)
})

onUnmounted(() => {
  // TODO: 學員需要在這裡清理事件監聽器
  // 提示：document.removeEventListener('keydown', handleKeydown)
})
</script>

<style scoped>
.self-challenge {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}



.practice-specs {
  background: #fff3e0;
  padding: 2rem;
  border-radius: 8px;
  margin: 2rem 0;
  border: 2px solid #ff9800;
}

.practice-specs h3 {
  color: #e65100;
  margin-bottom: 1.5rem;
}

.specs-container {
  display: flex;
  flex-direction: column;
  gap: 2rem;
}

.spec-item {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.spec-item h4 {
  color: #1976d2;
  margin-bottom: 1rem;
}

.task-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1rem;
  margin-top: 1rem;
}

.task-card {
  background: #f8f9fa;
  padding: 1.2rem;
  border-radius: 6px;
  border-left: 4px solid #4caf50;
}

.task-card h5 {
  color: #2e7d32;
  margin-bottom: 0.8rem;
}

.task-card ul {
  margin: 0.5rem 0;
  padding-left: 1.2rem;
}

.task-card li {
  margin: 0.3rem 0;
}

.hint {
  background: #e8f5e8;
  padding: 0.6rem;
  border-radius: 4px;
  margin-top: 0.8rem;
  font-size: 0.9rem;
}

.logic-explanation {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1rem;
}

.logic-item {
  background: #f3e5f5;
  padding: 1rem;
  border-radius: 6px;
}

.logic-item h6 {
  color: #7b1fa2;
  margin-bottom: 0.5rem;
}

.demo-section {
  margin: 2rem 0;
  padding: 1.5rem;
  border: 2px solid #4caf50;
  border-radius: 8px;
  background: #f1f8e9;
}

.counter-display {
  text-align: center;
  padding: 2rem;
  border-radius: 12px;
  margin: 2rem 0;
  transition: all 0.3s ease;
  cursor: pointer;
  position: relative;
}

.counter-normal {
  background: linear-gradient(135deg, #64b5f6, #42a5f5);
  color: white;
}

.counter-good {
  background: linear-gradient(135deg, #81c784, #66bb6a);
  color: white;
}

.counter-excellent {
  background: linear-gradient(135deg, #ffd54f, #ffca28);
  color: #333;
}

.mouse-inside {
  transform: scale(1.02);
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
}

.counter-value {
  font-size: 4rem;
  font-weight: bold;
  margin-bottom: 0.5rem;
}

.counter-label {
  font-size: 1.2rem;
  opacity: 0.9;
}

.mouse-position {
  position: absolute;
  top: 10px;
  right: 10px;
  font-size: 0.9rem;
  background: rgba(0, 0, 0, 0.1);
  padding: 0.3rem 0.6rem;
  border-radius: 4px;
}

.button-controls {
  display: flex;
  justify-content: center;
  gap: 1rem;
  margin: 2rem 0;
  flex-wrap: wrap;
}

.btn {
  padding: 1rem 1.5rem;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 1rem;
  font-weight: bold;
  transition: all 0.2s;
  min-width: 120px;
}

.btn-increase {
  background: #4caf50;
  color: white;
}

.btn-decrease {
  background: #f44336;
  color: white;
}

.btn-reset {
  background: #ff9800;
  color: white;
}

.btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.form-section {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  margin: 2rem 0;
  border: 1px solid #ddd;
}

.counter-form {
  display: flex;
  align-items: center;
  gap: 1rem;
  flex-wrap: wrap;
}

.counter-form label {
  font-weight: bold;
}

.counter-form input {
  padding: 0.5rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  width: 80px;
}

.counter-form button {
  padding: 0.5rem 1rem;
  background: #1976d2;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.context-menu-area {
  background: #e1f5fe;
  padding: 2rem;
  border-radius: 8px;
  margin: 2rem 0;
  text-align: center;
  position: relative;
  border: 2px dashed #0288d1;
}

.context-menu {
  position: fixed;
  background: white;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  z-index: 1000;
}

.menu-item {
  padding: 0.8rem 1.2rem;
  cursor: pointer;
  border-bottom: 1px solid #eee;
}

.menu-item:hover {
  background: #f5f5f5;
}

.menu-item:last-child {
  border-bottom: none;
}

.status-section {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  margin: 2rem 0;
  border: 1px solid #ddd;
}

.status-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
}

.status-item {
  display: flex;
  justify-content: space-between;
  padding: 0.5rem 0;
  border-bottom: 1px solid #eee;
}

.status-item label {
  font-weight: bold;
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
  padding: 0.8rem;
  background: #c8e6c9;
  border-radius: 4px;
}

.code-examples {
  margin-top: 1rem;
}

.code-examples h5 {
  color: #2e7d32;
  margin: 1.5rem 0 0.5rem 0;
}

pre {
  background: #2d3748;
  color: #e2e8f0;
  padding: 1rem;
  border-radius: 4px;
  overflow-x: auto;
  margin: 0.5rem 0;
}

kbd {
  background: #f5f5f5;
  border: 1px solid #ccc;
  border-radius: 3px;
  padding: 0.2rem 0.4rem;
  font-family: monospace;
  font-size: 0.9rem;
}

@media (max-width: 768px) {

  .task-grid,
  .logic-explanation,
  .status-grid {
    grid-template-columns: 1fr;
  }

  .counter-form {
    flex-direction: column;
    align-items: stretch;
  }

  .button-controls {
    flex-direction: column;
    align-items: center;
  }
}
</style>
