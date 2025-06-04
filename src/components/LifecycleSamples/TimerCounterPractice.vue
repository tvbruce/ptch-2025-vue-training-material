<template>
    <div class="timer-counter-practice">
        <h2>⏰ 計時器練習 - Lifecycle 生命週期</h2>
        <p class="route-info">📍 路徑：/LifecycleSamples/TimerCounterPractice.vue</p>
        <p class="description">
            📝 <strong>練習目標：</strong>學習 Vue 3 生命週期鉤子的使用，掌握組件掛載、更新、卸載的處理
        </p>

        <div class="demo-section">
            <h3>🎯 練習任務</h3>
            <div class="task-list">
                <div class="task-item">
                    <span>✅ 1. 使用 onMounted 開始計時器</span>
                </div>
                <div class="task-item">
                    <span>✅ 2. 使用 onBeforeUnmount 清理計時器</span>
                </div>
                <div class="task-item">
                    <span>✅ 3. 使用 watch 監聽數據變化</span>
                </div>
                <div class="task-item">
                    <span>✅ 4. 記錄生命週期執行順序</span>
                </div>
            </div>
        </div>

        <div class="demo-section">
            <h3>⏱️ 多功能計時器</h3>
            <div class="timer-container">
                <div class="timer-display">
                    <div class="main-timer">
                        <span class="timer-label">主計時器</span>
                        <span class="timer-value">{{ formatTime(mainTimer) }}</span>
                        <div class="timer-controls">
                            <button @click="toggleMainTimer"
                                :class="['btn', mainTimerRunning ? 'btn-warning' : 'btn-success']">
                                {{ mainTimerRunning ? '暫停' : '開始' }}
                            </button>
                            <button @click="resetMainTimer" class="btn btn-secondary">
                                重置
                            </button>
                        </div>
                    </div>

                    <div class="countdown-timer">
                        <span class="timer-label">倒數計時器</span>
                        <div class="countdown-input">
                            <input v-model.number="countdownMinutes" type="number" min="0" max="60"
                                class="input-field small" :disabled="countdownRunning"> 分
                            <input v-model.number="countdownSeconds" type="number" min="0" max="59"
                                class="input-field small" :disabled="countdownRunning"> 秒
                        </div>
                        <span class="timer-value" :class="{ 'timer-warning': countdown < 10 && countdownRunning }">
                            {{ formatTime(countdown) }}
                        </span>
                        <div class="timer-controls">
                            <button @click="toggleCountdown"
                                :class="['btn', countdownRunning ? 'btn-warning' : 'btn-success']"
                                :disabled="!countdownMinutes && !countdownSeconds && !countdownRunning">
                                {{ countdownRunning ? '暫停' : '開始' }}
                            </button>
                            <button @click="resetCountdown" class="btn btn-secondary">
                                重置
                            </button>
                        </div>
                    </div>
                </div>

                <div class="timer-stats">
                    <div class="stat-item">
                        <span class="stat-label">組件存活時間</span>
                        <span class="stat-value">{{ formatTime(componentLifetime) }}</span>
                    </div>
                    <div class="stat-item">
                        <span class="stat-label">主計時器總運行時間</span>
                        <span class="stat-value">{{ formatTime(totalMainTime) }}</span>
                    </div>
                    <div class="stat-item">
                        <span class="stat-label">倒數計時器完成次數</span>
                        <span class="stat-value">{{ countdownCompleted }} 次</span>
                    </div>
                </div>
            </div>
        </div>

        <div class="demo-section">
            <h3>📋 生命週期日誌</h3>
            <div class="lifecycle-log">
                <div v-for="(log, index) in lifecycleLogs" :key="index" class="log-entry"
                    :class="getLogClass(log.type)">
                    <span class="log-time">{{ log.time }}</span>
                    <span class="log-type">{{ log.type }}</span>
                    <span class="log-message">{{ log.message }}</span>
                </div>
            </div>
            <button @click="clearLogs" class="btn btn-secondary btn-sm">
                清空日誌
            </button>
        </div>

        <div class="code-example">
            <h4>💻 關鍵代碼</h4>
            <pre v-pre><code>import { ref, onMounted, onBeforeUnmount, watch } from 'vue'

// 生命週期鉤子
onMounted(() =&gt; {
  addLog('onMounted', '組件已掛載，開始計時器')
  startComponentTimer()
})

onBeforeUnmount(() =&gt; {
  addLog('onBeforeUnmount', '組件即將銷毀，清理計時器')
  clearAllTimers()
})

// 監聽器
watch(mainTimer, (newValue, oldValue) =&gt; {
  addLog('watch', `主計時器更新: ${oldValue} → ${newValue}`)
})

// 計時器管理
const startComponentTimer = () =&gt; {
  componentTimer = setInterval(() =&gt; {
    componentLifetime.value++
  }, 1000)
}

const clearAllTimers = () =&gt; {
  if (componentTimer) clearInterval(componentTimer)
  if (mainTimerInterval) clearInterval(mainTimerInterval)
  if (countdownInterval) clearInterval(countdownInterval)
}</code></pre>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, watch } from 'vue'

// 計時器數據
const mainTimer = ref(0)
const mainTimerRunning = ref(false)
const totalMainTime = ref(0)

const countdownMinutes = ref(1)
const countdownSeconds = ref(0)
const countdown = ref(0)
const countdownRunning = ref(false)
const countdownCompleted = ref(0)

const componentLifetime = ref(0)

// 生命週期日誌
const lifecycleLogs = ref([])

// 計時器引用
let componentTimer = null
let mainTimerInterval = null
let countdownInterval = null

// 生命週期鉤子
onMounted(() => {
    addLog('onMounted', '組件已掛載，開始記錄組件存活時間')
    startComponentTimer()
})

onBeforeUnmount(() => {
    addLog('onBeforeUnmount', '組件即將銷毀，清理所有計時器')
    clearAllTimers()
})

// 監聽器
watch(mainTimer, (newValue, oldValue) => {
    if (newValue !== oldValue && newValue % 10 === 0 && newValue > 0) {
        addLog('watch', `主計時器達到 ${newValue} 秒`)
    }
})

watch(countdown, (newValue) => {
    if (newValue === 0 && countdownRunning.value) {
        addLog('watch', '倒數計時器歸零！')
        countdownCompleted.value++
        countdownRunning.value = false
        clearInterval(countdownInterval)
        // 可以在這裡添加提醒音效或通知
        alert('倒數計時完成！')
    }
})

// 添加日誌
const addLog = (type, message) => {
    const now = new Date()
    lifecycleLogs.value.unshift({
        type,
        message,
        time: now.toLocaleTimeString()
    })

    // 限制日誌數量
    if (lifecycleLogs.value.length > 50) {
        lifecycleLogs.value.pop()
    }
}

// 格式化時間顯示
const formatTime = (seconds) => {
    const mins = Math.floor(seconds / 60)
    const secs = seconds % 60
    return `${mins.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`
}

// 組件存活時間計時器
const startComponentTimer = () => {
    componentTimer = setInterval(() => {
        componentLifetime.value++
    }, 1000)
}

// 主計時器控制
const toggleMainTimer = () => {
    if (mainTimerRunning.value) {
        clearInterval(mainTimerInterval)
        addLog('method', '主計時器已暫停')
    } else {
        mainTimerInterval = setInterval(() => {
            mainTimer.value++
            totalMainTime.value++
        }, 1000)
        addLog('method', '主計時器已開始')
    }
    mainTimerRunning.value = !mainTimerRunning.value
}

const resetMainTimer = () => {
    clearInterval(mainTimerInterval)
    mainTimer.value = 0
    mainTimerRunning.value = false
    addLog('method', '主計時器已重置')
}

// 倒數計時器控制
const toggleCountdown = () => {
    if (countdownRunning.value) {
        clearInterval(countdownInterval)
        addLog('method', '倒數計時器已暫停')
    } else {
        if (countdown.value === 0) {
            countdown.value = countdownMinutes.value * 60 + countdownSeconds.value
        }
        countdownInterval = setInterval(() => {
            if (countdown.value > 0) {
                countdown.value--
            }
        }, 1000)
        addLog('method', `倒數計時器已開始，設定時間 ${formatTime(countdown.value)}`)
    }
    countdownRunning.value = !countdownRunning.value
}

const resetCountdown = () => {
    clearInterval(countdownInterval)
    countdown.value = 0
    countdownRunning.value = false
    addLog('method', '倒數計時器已重置')
}

// 清理所有計時器
const clearAllTimers = () => {
    if (componentTimer) clearInterval(componentTimer)
    if (mainTimerInterval) clearInterval(mainTimerInterval)
    if (countdownInterval) clearInterval(countdownInterval)
}

// 清空日誌
const clearLogs = () => {
    lifecycleLogs.value = []
    addLog('method', '日誌已清空')
}

// 獲取日誌樣式類
const getLogClass = (type) => {
    const classes = {
        'onMounted': 'log-mounted',
        'onBeforeUnmount': 'log-unmount',
        'watch': 'log-watch',
        'method': 'log-method'
    }
    return classes[type] || ''
}
</script>

<style scoped>
.timer-container {
    background: #f8f9fa;
    padding: 1.5rem;
    border-radius: 12px;
    margin: 1rem 0;
}

.timer-display {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
    margin-bottom: 2rem;
}

.main-timer,
.countdown-timer {
    background: white;
    padding: 1.5rem;
    border-radius: 8px;
    text-align: center;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.timer-label {
    display: block;
    font-size: 0.9rem;
    font-weight: bold;
    color: #666;
    margin-bottom: 1rem;
}

.timer-value {
    display: block;
    font-size: 3rem;
    font-weight: bold;
    color: #2c3e50;
    margin-bottom: 1rem;
    font-family: 'Courier New', monospace;
}

.timer-warning {
    color: #e74c3c;
    animation: pulse 1s infinite;
}

@keyframes pulse {

    0%,
    100% {
        opacity: 1;
    }

    50% {
        opacity: 0.5;
    }
}

.countdown-input {
    display: flex;
    justify-content: center;
    gap: 0.5rem;
    align-items: center;
    margin-bottom: 1rem;
}

.input-field.small {
    width: 60px;
    text-align: center;
}

.timer-controls {
    display: flex;
    gap: 0.5rem;
    justify-content: center;
}

.timer-stats {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1rem;
}

.stat-item {
    background: linear-gradient(135deg, #74b9ff, #0984e3);
    color: white;
    padding: 1rem;
    border-radius: 8px;
    text-align: center;
}

.stat-label {
    display: block;
    font-size: 0.9rem;
    margin-bottom: 0.5rem;
    opacity: 0.9;
}

.stat-value {
    display: block;
    font-size: 1.5rem;
    font-weight: bold;
}

.lifecycle-log {
    background: #2c3e50;
    color: #ecf0f1;
    padding: 1rem;
    border-radius: 8px;
    max-height: 300px;
    overflow-y: auto;
    font-family: 'Courier New', monospace;
    font-size: 0.9rem;
}

.log-entry {
    display: flex;
    gap: 1rem;
    padding: 0.25rem 0;
    border-bottom: 1px solid #34495e;
}

.log-time {
    color: #95a5a6;
    min-width: 80px;
}

.log-type {
    min-width: 120px;
    font-weight: bold;
}

.log-mounted .log-type {
    color: #2ecc71;
}

.log-unmount .log-type {
    color: #e74c3c;
}

.log-watch .log-type {
    color: #f39c12;
}

.log-method .log-type {
    color: #3498db;
}

.log-message {
    flex: 1;
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
    .timer-display {
        grid-template-columns: 1fr;
    }

    .timer-value {
        font-size: 2rem;
    }
}
</style>
