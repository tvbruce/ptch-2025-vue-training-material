<template>
    <div class="solution">
        <h2>✅ 解答 - Lifecycle 生命週期</h2>
        <p>完整實現生命週期管理系統，展示各種生命週期鉤子的用法</p>

        <!-- 計時器功能 -->
        <div class="demo-card">
            <h4>計時器功能</h4>
            <div class="timer-display">
                <div class="time-value">{{ formatTime(timerSeconds) }}</div>
                <div class="timer-controls">
                    <button @click="toggleTimer" :class="{ active: isTimerRunning }">
                        {{ isTimerRunning ? '暫停' : '開始' }}
                    </button>
                    <button @click="resetTimer" class="reset-btn">重置</button>
                </div>
                <div class="timer-status">
                    狀態：{{ isTimerRunning ? '運行中' : '已停止' }}
                </div>
            </div>
        </div>

        <!-- 用戶資料載入 -->
        <div class="demo-card">
            <h4>用戶資料載入</h4>
            <div v-if="isLoading" class="loading-state">
                <div class="spinner"></div>
                <p>載入中...</p>
            </div>

            <div v-else class="user-data">
                <h5>用戶列表 ({{ userData.length }} 位用戶)</h5>
                <div class="user-grid">
                    <div v-for="user in userData" :key="user.id" class="user-card">
                        <h6>{{ user.name }}</h6>
                        <p>{{ user.email }}</p>
                        <p>ID: {{ user.id }}</p>
                    </div>
                </div>
                <button @click="loadUserData" class="reload-btn">重新載入</button>
            </div>
        </div>

        <!-- 組件更新計數 -->
        <div class="demo-card">
            <h4>組件更新計數</h4>
            <div class="update-info">
                <p><strong>更新次數：</strong>{{ updateCount }}</p>
                <p><strong>計時器秒數：</strong>{{ timerSeconds }}</p>
                <p><strong>用戶數量：</strong>{{ userData.length }}</p>
                <div class="update-triggers">
                    <button @click="triggerUpdate">觸發更新</button>
                    <button @click="addRandomUser">新增用戶</button>
                </div>
            </div>
        </div>

        <!-- 生命週期日誌 -->
        <div class="demo-card">
            <h4>生命週期日誌</h4>
            <div class="lifecycle-logs">
                <div v-for="(log, index) in lifecycleLogs" :key="index" class="log-entry">
                    <span class="log-time">{{ log.time }}</span>
                    <span class="log-event">{{ log.event }}</span>
                    <span class="log-message">{{ log.message }}</span>
                </div>
            </div>
            <button @click="clearLogs" class="clear-btn">清除日誌</button>
        </div>

        <!-- 資源狀態 -->
        <div class="demo-card">
            <h4>資源狀態</h4>
            <div class="resource-status">
                <div class="status-item">
                    <span class="status-label">計時器 ID：</span>
                    <span class="status-value">{{ intervalId || '無' }}</span>
                </div>
                <div class="status-item">
                    <span class="status-label">組件掛載：</span>
                    <span class="status-value">{{ isMounted ? '是' : '否' }}</span>
                </div>
                <div class="status-item">
                    <span class="status-label">資料載入：</span>
                    <span class="status-value">{{ isLoading ? '載入中' : '完成' }}</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, onUpdated } from 'vue'

// 計時器相關
const timerSeconds = ref(0)
const isTimerRunning = ref(false)
const intervalId = ref(null)

// 用戶資料相關
const userData = ref([])
const isLoading = ref(true)

// 組件狀態
const updateCount = ref(0)
const isMounted = ref(false)
const lifecycleLogs = ref([])

// 1. formatTime 函數
const formatTime = (seconds) => {
    const minutes = Math.floor(seconds / 60)
    const remainingSeconds = seconds % 60
    return `${minutes.toString().padStart(2, '0')}:${remainingSeconds.toString().padStart(2, '0')}`
}

// 2. toggleTimer 函數
const toggleTimer = () => {
    if (isTimerRunning.value) {
        // 暫停計時器
        if (intervalId.value) {
            clearInterval(intervalId.value)
            intervalId.value = null
        }
        isTimerRunning.value = false
        addLog('Timer', '計時器已暫停')
    } else {
        // 開始計時器
        intervalId.value = setInterval(() => {
            timerSeconds.value++
        }, 1000)
        isTimerRunning.value = true
        addLog('Timer', '計時器已開始')
    }
}

// 3. resetTimer 函數
const resetTimer = () => {
    if (intervalId.value) {
        clearInterval(intervalId.value)
        intervalId.value = null
    }
    timerSeconds.value = 0
    isTimerRunning.value = false
    addLog('Timer', '計時器已重置')
}

// 4. loadUserData 函數
const loadUserData = () => {
    isLoading.value = true
    addLog('Data', '開始載入用戶資料')

    // 模擬 API 載入延遲
    setTimeout(() => {
        userData.value = [
            { id: 1, name: '張小明', email: 'zhang@example.com' },
            { id: 2, name: '李小華', email: 'li@example.com' },
            { id: 3, name: '王小美', email: 'wang@example.com' },
            { id: 4, name: '陳小強', email: 'chen@example.com' },
            { id: 5, name: '林小雅', email: 'lin@example.com' }
        ]
        isLoading.value = false
        addLog('Data', `用戶資料載入完成，共 ${userData.value.length} 位用戶`)
    }, 2000)
}

// 輔助函數
const addLog = (event, message) => {
    lifecycleLogs.value.unshift({
        time: new Date().toLocaleTimeString(),
        event,
        message
    })

    // 限制日誌數量
    if (lifecycleLogs.value.length > 20) {
        lifecycleLogs.value = lifecycleLogs.value.slice(0, 20)
    }
}

const triggerUpdate = () => {
    // 觸發組件更新
    timerSeconds.value = timerSeconds.value
}

const addRandomUser = () => {
    const newUser = {
        id: userData.value.length + 1,
        name: `用戶${userData.value.length + 1}`,
        email: `user${userData.value.length + 1}@example.com`
    }
    userData.value.push(newUser)
    addLog('Data', `新增用戶：${newUser.name}`)
}

const clearLogs = () => {
    lifecycleLogs.value = []
}

// 5. onMounted 生命週期
onMounted(() => {
    isMounted.value = true
    addLog('Lifecycle', '組件已掛載 (onMounted)')

    // 自動載入用戶資料
    loadUserData()

    console.log('組件已掛載')
})

// 6. onUnmounted 生命週期
onUnmounted(() => {
    // 清理計時器
    if (intervalId.value) {
        clearInterval(intervalId.value)
    }

    addLog('Lifecycle', '組件即將卸載 (onUnmounted)')
    console.log('組件已卸載，資源已清理')
})

// 7. onUpdated 生命週期
onUpdated(() => {
    updateCount.value++
    addLog('Lifecycle', `組件已更新 (onUpdated) - 第 ${updateCount.value} 次`)
})
</script>

<style scoped>
.solution {
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
}

.demo-card {
    background: white;
    border: 1px solid #e9ecef;
    border-radius: 10px;
    padding: 20px;
    margin-bottom: 20px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.timer-display {
    text-align: center;
}

.time-value {
    font-size: 3em;
    font-weight: bold;
    color: #495057;
    margin-bottom: 20px;
    font-family: 'Courier New', monospace;
}

.timer-controls {
    display: flex;
    gap: 10px;
    justify-content: center;
    margin-bottom: 15px;
}

.timer-controls button {
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-weight: 500;
    transition: all 0.2s;
}

.timer-controls button:first-child {
    background: #28a745;
    color: white;
}

.timer-controls button:first-child.active {
    background: #ffc107;
    color: #212529;
}

.reset-btn {
    background: #dc3545 !important;
    color: white !important;
}

.timer-status {
    color: #6c757d;
    font-size: 0.9em;
}

.loading-state {
    text-align: center;
    padding: 40px;
}

.spinner {
    width: 40px;
    height: 40px;
    border: 4px solid #f3f3f3;
    border-top: 4px solid #007bff;
    border-radius: 50%;
    animation: spin 1s linear infinite;
    margin: 0 auto 20px;
}

@keyframes spin {
    0% {
        transform: rotate(0deg);
    }

    100% {
        transform: rotate(360deg);
    }
}

.user-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 15px;
    margin: 15px 0;
}

.user-card {
    padding: 15px;
    border: 1px solid #e9ecef;
    border-radius: 8px;
    background: #f8f9fa;
}

.user-card h6 {
    margin: 0 0 8px 0;
    color: #495057;
}

.user-card p {
    margin: 4px 0;
    color: #6c757d;
    font-size: 0.9em;
}

.reload-btn {
    padding: 8px 16px;
    background: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

.update-info {
    background: #f8f9fa;
    padding: 20px;
    border-radius: 8px;
}

.update-info p {
    margin: 8px 0;
    color: #495057;
}

.update-triggers {
    display: flex;
    gap: 10px;
    margin-top: 15px;
}

.update-triggers button {
    padding: 8px 16px;
    background: #17a2b8;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

.lifecycle-logs {
    max-height: 300px;
    overflow-y: auto;
    border: 1px solid #e9ecef;
    border-radius: 5px;
    padding: 10px;
    background: #f8f9fa;
}

.log-entry {
    display: grid;
    grid-template-columns: 80px 100px 1fr;
    gap: 10px;
    padding: 5px 0;
    border-bottom: 1px solid #e9ecef;
    font-size: 0.9em;
}

.log-entry:last-child {
    border-bottom: none;
}

.log-time {
    color: #6c757d;
    font-family: 'Courier New', monospace;
}

.log-event {
    color: #007bff;
    font-weight: 500;
}

.log-message {
    color: #495057;
}

.clear-btn {
    padding: 8px 16px;
    background: #6c757d;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    margin-top: 10px;
}

.resource-status {
    display: grid;
    gap: 10px;
}

.status-item {
    display: flex;
    justify-content: space-between;
    padding: 10px 15px;
    background: #f8f9fa;
    border-radius: 5px;
}

.status-label {
    color: #6c757d;
    font-weight: 500;
}

.status-value {
    color: #495057;
    font-weight: bold;
}

button:hover {
    opacity: 0.8;
}

@media (max-width: 768px) {
    .timer-controls {
        flex-direction: column;
        align-items: center;
    }

    .update-triggers {
        flex-direction: column;
    }

    .user-grid {
        grid-template-columns: 1fr;
    }

    .log-entry {
        grid-template-columns: 1fr;
        gap: 5px;
    }
}
</style>
