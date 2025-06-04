<template>
    <div class="interactive-game-practice">
        <h2>🎮 互動小遊戲 - Event 事件處理練習</h2>
        <p class="route-info">📍 路徑：/EventHandlingSamples/InteractiveGamePractice.vue</p>
        <p class="description">
            📝 <strong>練習目標：</strong>學習 Vue 3 事件處理，掌握點擊、鍵盤、鼠標事件及事件修飾符
        </p>

        <div class="demo-section">
            <h3>🎯 練習任務</h3>
            <div class="task-list">
                <div class="task-item">
                    <span>✅ 1. 滑鼠點擊事件處理</span>
                </div>
                <div class="task-item">
                    <span>✅ 2. 鍵盤事件與按鍵修飾符</span>
                </div>
                <div class="task-item">
                    <span>✅ 3. 滑鼠移動事件追蹤</span>
                </div>
                <div class="task-item">
                    <span>✅ 4. 事件修飾符應用</span>
                </div>
                <div class="task-item">
                    <span>✅ 5. 事件參數傳遞</span>
                </div>
            </div>
        </div>

        <!-- 遊戲選擇 -->
        <div class="demo-section">
            <h3>🎲 選擇遊戲</h3>
            <div class="game-selector">
                <button v-for="game in games" :key="game.id" @click="selectGame(game.id)"
                    :class="['btn', 'game-btn', { 'active': currentGame === game.id }]">
                    {{ game.emoji }} {{ game.name }}
                </button>
            </div>
        </div>

        <!-- 點擊遊戲 -->
        <div v-if="currentGame === 'click'" class="demo-section">
            <h3>🖱️ 點擊大挑戰</h3>
            <div class="click-game">
                <div class="game-stats">
                    <div class="stat">點擊次數: {{ clickCount }}</div>
                    <div class="stat">剩餘時間: {{ clickTimeLeft }}s</div>
                    <div class="stat">最高紀錄: {{ clickHighScore }}</div>
                </div>

                <div class="click-area" @click="handleClick">
                    <div v-for="(target, index) in clickTargets" :key="index" class="click-target" :style="{
                        left: target.x + 'px',
                        top: target.y + 'px',
                        backgroundColor: target.color
                    }" @click.stop="hitTarget(index)">
                        {{ target.emoji }}
                    </div>
                    <div v-if="!clickGameActive" class="game-overlay">
                        <div class="overlay-content">
                            <h4>{{ clickTimeLeft === 0 ? '時間到！' : '點擊大挑戰' }}</h4>
                            <p>在 {{ clickGameDuration }} 秒內盡可能多地點擊目標</p>
                            <button @click="startClickGame" class="btn btn-primary">
                                {{ clickTimeLeft === 0 ? '重新開始' : '開始遊戲' }}
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- 鍵盤遊戲 -->
        <div v-if="currentGame === 'keyboard'" class="demo-section">
            <h3>⌨️ 鍵盤反應測試</h3>
            <div class="keyboard-game">
                <div class="game-stats">
                    <div class="stat">正確數: {{ keyboardScore }}</div>
                    <div class="stat">錯誤數: {{ keyboardErrors }}</div>
                    <div class="stat">準確率: {{ keyboardAccuracy }}%</div>
                </div>

                <div class="keyboard-area" tabindex="0" @keyup="handleKeyPress" @focus="keyboardFocused = true"
                    @blur="keyboardFocused = false">
                    <div v-if="!keyboardFocused" class="focus-hint">
                        點擊這裡開始，然後按下顯示的按鍵
                    </div>
                    <div v-else class="key-display">
                        <div class="target-key">{{ currentTargetKey }}</div>
                        <div class="key-hint">按下此按鍵</div>
                    </div>

                    <div class="pressed-keys">
                        <div v-for="(key, index) in recentKeys" :key="index" class="pressed-key"
                            :class="{ 'correct': key.correct, 'incorrect': !key.correct }">
                            {{ key.key }}
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- 滑鼠追蹤遊戲 -->
        <div v-if="currentGame === 'mouse'" class="demo-section">
            <h3>🎯 滑鼠精準度測試</h3>
            <div class="mouse-game">
                <div class="game-stats">
                    <div class="stat">命中數: {{ mouseHits }}</div>
                    <div class="stat">總嘗試: {{ mouseAttempts }}</div>
                    <div class="stat">命中率: {{ mouseAccuracy }}%</div>
                </div>

                <div class="mouse-area" @mousemove="trackMouse" @click="handleMouseClick">
                    <!-- 滑鼠軌跡 -->
                    <svg class="mouse-trail" width="100%" height="100%">
                        <path v-if="mouseTrail.length > 1" :d="mouseTrailPath" stroke="#3498db" stroke-width="2"
                            fill="none" opacity="0.6" />
                    </svg>

                    <!-- 目標圓圈 -->
                    <div v-for="(circle, index) in mouseTargets" :key="index" class="mouse-target" :style="{
                        left: circle.x - circle.radius + 'px',
                        top: circle.y - circle.radius + 'px',
                        width: circle.radius * 2 + 'px',
                        height: circle.radius * 2 + 'px'
                    }" @click.stop="hitMouseTarget(index)">
                        {{ circle.points }}
                    </div>

                    <!-- 滑鼠位置指示器 -->
                    <div class="mouse-cursor" :style="{
                        left: mousePosition.x - 5 + 'px',
                        top: mousePosition.y - 5 + 'px'
                    }"></div>
                </div>

                <div class="mouse-controls">
                    <button @click="generateMouseTargets" class="btn btn-primary">
                        生成新目標
                    </button>
                    <button @click="clearMouseTrail" class="btn btn-secondary">
                        清除軌跡
                    </button>
                </div>
            </div>
        </div>

        <!-- 事件修飾符演示 -->
        <div v-if="currentGame === 'modifiers'" class="demo-section">
            <h3>🔧 事件修飾符演示</h3>
            <div class="modifiers-demo">
                <div class="modifier-example">
                    <h4>.stop 修飾符</h4>
                    <div class="outer-box" @click="outerClick">
                        外層容器 (會觸發)
                        <div class="inner-box" @click.stop="innerClick">
                            內層容器 (.stop)
                        </div>
                    </div>
                    <div class="event-log">{{ stopLog }}</div>
                </div>

                <div class="modifier-example">
                    <h4>.prevent 修飾符</h4>
                    <form @submit.prevent="handleSubmit">
                        <input v-model="formInput" placeholder="輸入內容">
                        <button type="submit">提交 (.prevent)</button>
                    </form>
                    <div class="event-log">{{ preventLog }}</div>
                </div>

                <div class="modifier-example">
                    <h4>.once 修飾符</h4>
                    <button @click.once="onceClick">
                        只能點擊一次 (.once)
                    </button>
                    <div class="event-log">{{ onceLog }}</div>
                </div>

                <div class="modifier-example">
                    <h4>按鍵修飾符</h4>
                    <input v-model="keyInput" @keyup.enter="enterPress" @keyup.esc="escPress" @keyup.space="spacePress"
                        placeholder="試試 Enter、Esc、Space 鍵">
                    <div class="event-log">{{ keyLog }}</div>
                </div>
            </div>
        </div>

        <div class="code-example">
            <h4>💻 關鍵代碼</h4>
            <pre v-pre><code>// 基本事件處理
&lt;button @click="handleClick"&gt;點擊我&lt;/button&gt;

// 鍵盤事件
&lt;input @keyup="handleKeyPress"&gt;
&lt;input @keyup.enter="handleEnter"&gt;

// 滑鼠事件
&lt;div @mousemove="trackMouse"&gt;&lt;/div&gt;

// 事件修飾符
&lt;div @click.stop="stopPropagation"&gt;&lt;/div&gt;
&lt;form @submit.prevent="preventSubmit"&gt;&lt;/form&gt;
&lt;button @click.once="onlyOnce"&gt;&lt;/button&gt;

// 事件處理方法
const handleClick = (event) =&gt; {
  console.log('點擊事件', event)
}

const handleKeyPress = (event) =&gt; {
  console.log('按鍵事件', event.key)
}</code></pre>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, onMounted, onBeforeUnmount } from 'vue'

// 遊戲列表
const games = [
    { id: 'click', name: '點擊大挑戰', emoji: '🖱️' },
    { id: 'keyboard', name: '鍵盤反應', emoji: '⌨️' },
    { id: 'mouse', name: '滑鼠精準度', emoji: '🎯' },
    { id: 'modifiers', name: '事件修飾符', emoji: '🔧' }
]

const currentGame = ref('click')

// 點擊遊戲
const clickCount = ref(0)
const clickTimeLeft = ref(0)
const clickGameActive = ref(false)
const clickGameDuration = 10
const clickTargets = ref([])
const clickHighScore = ref(localStorage.getItem('clickHighScore') || 0)
let clickTimer = null

// 鍵盤遊戲
const keyboardScore = ref(0)
const keyboardErrors = ref(0)
const keyboardFocused = ref(false)
const currentTargetKey = ref('')
const recentKeys = ref([])
const possibleKeys = ['A', 'S', 'D', 'F', 'J', 'K', 'L', 'Q', 'W', 'E', 'R']

// 滑鼠遊戲
const mouseHits = ref(0)
const mouseAttempts = ref(0)
const mousePosition = ref({ x: 0, y: 0 })
const mouseTrail = ref([])
const mouseTargets = ref([])

// 事件修飾符演示
const stopLog = ref('')
const preventLog = ref('')
const onceLog = ref('')
const keyLog = ref('')
const formInput = ref('')
const keyInput = ref('')

// 計算屬性
const keyboardAccuracy = computed(() => {
    const total = keyboardScore.value + keyboardErrors.value
    return total === 0 ? 0 : Math.round((keyboardScore.value / total) * 100)
})

const mouseAccuracy = computed(() => {
    return mouseAttempts.value === 0 ? 0 : Math.round((mouseHits.value / mouseAttempts.value) * 100)
})

const mouseTrailPath = computed(() => {
    if (mouseTrail.value.length < 2) return ''

    let path = `M ${mouseTrail.value[0].x} ${mouseTrail.value[0].y}`
    for (let i = 1; i < mouseTrail.value.length; i++) {
        path += ` L ${mouseTrail.value[i].x} ${mouseTrail.value[i].y}`
    }
    return path
})

// 遊戲選擇
const selectGame = (gameId) => {
    currentGame.value = gameId
    if (gameId === 'keyboard') {
        generateTargetKey()
    } else if (gameId === 'mouse') {
        generateMouseTargets()
    }
}

// 點擊遊戲方法
const startClickGame = () => {
    clickCount.value = 0
    clickTimeLeft.value = clickGameDuration
    clickGameActive.value = true
    generateClickTargets()

    clickTimer = setInterval(() => {
        clickTimeLeft.value--
        if (clickTimeLeft.value <= 0) {
            endClickGame()
        }
    }, 1000)
}

const endClickGame = () => {
    clickGameActive.value = false
    if (clickTimer) clearInterval(clickTimer)

    if (clickCount.value > clickHighScore.value) {
        clickHighScore.value = clickCount.value
        localStorage.setItem('clickHighScore', clickCount.value)
    }

    clickTargets.value = []
}

const generateClickTargets = () => {
    clickTargets.value = []
    for (let i = 0; i < 3; i++) {
        clickTargets.value.push({
            x: Math.random() * 350,
            y: Math.random() * 250,
            color: getRandomColor(),
            emoji: getRandomEmoji()
        })
    }
}

const handleClick = () => {
    if (clickGameActive.value) {
        // 點擊空白區域不計分
    }
}

const hitTarget = (index) => {
    if (clickGameActive.value) {
        clickCount.value++
        // 重新生成目標
        clickTargets.value[index] = {
            x: Math.random() * 350,
            y: Math.random() * 250,
            color: getRandomColor(),
            emoji: getRandomEmoji()
        }
    }
}

// 鍵盤遊戲方法
const generateTargetKey = () => {
    currentTargetKey.value = possibleKeys[Math.floor(Math.random() * possibleKeys.length)]
}

const handleKeyPress = (event) => {
    if (!keyboardFocused.value) return

    const pressedKey = event.key.toUpperCase()
    const isCorrect = pressedKey === currentTargetKey.value

    recentKeys.value.unshift({
        key: pressedKey,
        correct: isCorrect
    })

    if (recentKeys.value.length > 10) {
        recentKeys.value.pop()
    }

    if (isCorrect) {
        keyboardScore.value++
    } else {
        keyboardErrors.value++
    }

    generateTargetKey()
}

// 滑鼠遊戲方法
const trackMouse = (event) => {
    const rect = event.currentTarget.getBoundingClientRect()
    mousePosition.value = {
        x: event.clientX - rect.left,
        y: event.clientY - rect.top
    }

    mouseTrail.value.push({ ...mousePosition.value })
    if (mouseTrail.value.length > 50) {
        mouseTrail.value.shift()
    }
}

const handleMouseClick = () => {
    mouseAttempts.value++
}

const hitMouseTarget = (index) => {
    mouseHits.value++
    mouseTargets.value.splice(index, 1)

    // 自動生成新目標
    if (mouseTargets.value.length < 3) {
        generateMouseTargets()
    }
}

const generateMouseTargets = () => {
    mouseTargets.value = []
    for (let i = 0; i < 5; i++) {
        mouseTargets.value.push({
            x: 50 + Math.random() * 350,
            y: 50 + Math.random() * 200,
            radius: 20 + Math.random() * 30,
            points: Math.floor(Math.random() * 9) + 1
        })
    }
}

const clearMouseTrail = () => {
    mouseTrail.value = []
}

// 事件修飾符演示方法
const outerClick = () => {
    stopLog.value = '外層容器被點擊'
}

const innerClick = () => {
    stopLog.value = '內層容器被點擊 (事件不會冒泡)'
}

const handleSubmit = () => {
    preventLog.value = `表單提交被阻止，輸入內容: ${formInput.value}`
}

const onceClick = () => {
    onceLog.value = '這個按鈕只能被點擊一次'
}

const enterPress = () => {
    keyLog.value = '按下了 Enter 鍵'
}

const escPress = () => {
    keyLog.value = '按下了 Esc 鍵'
}

const spacePress = () => {
    keyLog.value = '按下了 Space 鍵'
}

// 工具函數
const getRandomColor = () => {
    const colors = ['#e74c3c', '#3498db', '#2ecc71', '#f39c12', '#9b59b6', '#1abc9c']
    return colors[Math.floor(Math.random() * colors.length)]
}

const getRandomEmoji = () => {
    const emojis = ['🎯', '⭐', '💎', '🏆', '🎊', '🔥', '⚡', '🎈']
    return emojis[Math.floor(Math.random() * emojis.length)]
}

// 生命週期
onMounted(() => {
    generateTargetKey()
    generateMouseTargets()
})

onBeforeUnmount(() => {
    if (clickTimer) clearInterval(clickTimer)
})
</script>

<style scoped>
.game-selector {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    margin: 1rem 0;
}

.game-btn {
    padding: 1rem 1.5rem;
    font-size: 1.1rem;
    border-radius: 8px;
    transition: all 0.3s;
}

.game-btn.active {
    background: #3498db;
    color: white;
    transform: scale(1.05);
}

.click-game,
.keyboard-game,
.mouse-game {
    background: white;
    padding: 1.5rem;
    border-radius: 12px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.game-stats {
    display: flex;
    gap: 2rem;
    margin-bottom: 1.5rem;
    justify-content: center;
}

.stat {
    background: #f8f9fa;
    padding: 0.75rem 1.5rem;
    border-radius: 8px;
    font-weight: bold;
    color: #2c3e50;
}

.click-area,
.keyboard-area,
.mouse-area {
    position: relative;
    width: 100%;
    height: 300px;
    border: 3px dashed #ddd;
    border-radius: 8px;
    overflow: hidden;
}

.click-target {
    position: absolute;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.5rem;
    cursor: pointer;
    transition: transform 0.1s;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
}

.click-target:hover {
    transform: scale(1.1);
}

.game-overlay {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.8);
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
}

.overlay-content {
    text-align: center;
}

.keyboard-area {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    background: #f8f9fa;
}

.keyboard-area:focus {
    outline: 3px solid #3498db;
    background: white;
}

.focus-hint {
    color: #666;
    font-size: 1.1rem;
}

.key-display {
    text-align: center;
}

.target-key {
    font-size: 4rem;
    font-weight: bold;
    color: #3498db;
    margin-bottom: 1rem;
}

.key-hint {
    font-size: 1.2rem;
    color: #666;
}

.pressed-keys {
    display: flex;
    gap: 0.5rem;
    margin-top: 2rem;
}

.pressed-key {
    padding: 0.5rem;
    border-radius: 4px;
    font-weight: bold;
    min-width: 30px;
    text-align: center;
}

.pressed-key.correct {
    background: #2ecc71;
    color: white;
}

.pressed-key.incorrect {
    background: #e74c3c;
    color: white;
}

.mouse-area {
    background: #f8f9fa;
    cursor: crosshair;
}

.mouse-trail {
    position: absolute;
    top: 0;
    left: 0;
    pointer-events: none;
}

.mouse-target {
    position: absolute;
    background: #e74c3c;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    font-weight: bold;
    cursor: pointer;
    transition: transform 0.1s;
    border: 3px solid #c0392b;
}

.mouse-target:hover {
    transform: scale(1.1);
}

.mouse-cursor {
    position: absolute;
    width: 10px;
    height: 10px;
    background: #3498db;
    border-radius: 50%;
    pointer-events: none;
}

.mouse-controls {
    display: flex;
    gap: 1rem;
    justify-content: center;
    margin-top: 1rem;
}

.modifiers-demo {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1.5rem;
}

.modifier-example {
    background: white;
    padding: 1.5rem;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.outer-box {
    background: #3498db;
    color: white;
    padding: 2rem;
    border-radius: 8px;
    cursor: pointer;
    text-align: center;
}

.inner-box {
    background: #e74c3c;
    padding: 1rem;
    border-radius: 4px;
    margin-top: 1rem;
    cursor: pointer;
}

.event-log {
    background: #f8f9fa;
    padding: 1rem;
    border-radius: 4px;
    margin-top: 1rem;
    font-family: monospace;
    min-height: 50px;
    display: flex;
    align-items: center;
}

.task-list {
    background: #f8f9fa;
    padding: 1rem;
    border-radius: 8px;
    margin: 1rem 0;
}

.task-item {
    padding: 0.5rem 0;
    color: #28a745;
}

@media (max-width: 768px) {
    .game-stats {
        flex-direction: column;
        gap: 1rem;
    }

    .modifiers-demo {
        grid-template-columns: 1fr;
    }
}
</style>
