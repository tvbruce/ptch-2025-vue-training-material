<template>
    <div class="parent-component">
        <div class="demo-header">
            <h4>📡 父子組件通信演示</h4>
            <p>展示複雜的組件間數據傳遞和事件通信</p>
        </div>

        <!-- 通信狀態面板 -->
        <div class="communication-panel">
            <h5>📊 通信狀態</h5>
            <div class="status-grid">
                <div class="status-item">
                    <span class="status-label">父組件消息:</span>
                    <span class="status-value">{{ parentMessage }}</span>
                </div>
                <div class="status-item">
                    <span class="status-label">子組件回應:</span>
                    <span class="status-value">{{ childResponse }}</span>
                </div>
                <div class="status-item">
                    <span class="status-label">通信次數:</span>
                    <span class="status-value">{{ communicationCount }} 次</span>
                </div>
                <div class="status-item">
                    <span class="status-label">最後通信:</span>
                    <span class="status-value">{{ lastCommunicationTime }}</span>
                </div>
            </div>
        </div>

        <!-- 父組件控制面板 -->
        <div class="control-panel">
            <h5>🎮 父組件控制</h5>
            <div class="control-actions">
                <div class="input-group">
                    <label>發送消息給子組件:</label>
                    <div class="input-with-button">
                        <input v-model="messageToChild" type="text" placeholder="輸入要發送的消息..." class="message-input"
                            @keyup.enter="sendMessageToChild" />
                        <button @click="sendMessageToChild" class="send-btn">
                            📤 發送
                        </button>
                    </div>
                </div>

                <div class="button-group">
                    <button @click="updateChildData" class="control-btn update-btn">
                        🔄 更新子組件數據
                    </button>
                    <button @click="resetChildState" class="control-btn reset-btn">
                        🔄 重置子組件狀態
                    </button>
                    <button @click="toggleChildVisibility" class="control-btn toggle-btn">
                        {{ showChild ? '👁️ 隱藏子組件' : '👁️ 顯示子組件' }}
                    </button>
                </div>
            </div>
        </div>

        <!-- 子組件區域 -->
        <div v-if="showChild" class="child-area">
            <h5>👶 子組件區域</h5>
            <ChildComponent :parent-message="parentMessage" :shared-data="sharedData" :config="childConfig"
                @child-message="handleChildMessage" @data-updated="handleDataUpdated"
                @status-changed="handleStatusChanged" @task-completed="handleTaskCompleted" />
        </div>

        <!-- 通信日誌 -->
        <div class="communication-log">
            <h5>📝 通信日誌</h5>
            <div class="log-controls">
                <button @click="clearLog" class="clear-btn">🗑️ 清空日誌</button>
                <button @click="exportLog" class="export-btn">📤 導出日誌</button>
            </div>
            <div class="log-container">
                <div v-for="(log, index) in communicationLog" :key="index" class="log-entry" :class="log.type">
                    <div class="log-time">{{ log.time }}</div>
                    <div class="log-type">{{ log.typeText }}</div>
                    <div class="log-message">{{ log.message }}</div>
                </div>
                <div v-if="communicationLog.length === 0" class="empty-log">
                    暫無通信記錄
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import ChildComponent from './ChildComponent.vue'

// 定義事件發射
const emit = defineEmits(['task-completed'])

// 響應式數據
const parentMessage = ref('歡迎使用組件通信演示！')
const childResponse = ref('等待子組件回應...')
const messageToChild = ref('')
const communicationCount = ref(0)
const lastCommunicationTime = ref('尚未開始')
const showChild = ref(true)

// 共享數據
const sharedData = ref({
    counter: 0,
    items: ['項目1', '項目2', '項目3'],
    settings: {
        theme: 'light',
        language: 'zh-TW'
    }
})

// 子組件配置
const childConfig = ref({
    allowEdit: true,
    maxItems: 10,
    autoSave: true
})

// 通信日誌
const communicationLog = ref([])

// 方法
const sendMessageToChild = () => {
    if (messageToChild.value.trim()) {
        parentMessage.value = messageToChild.value.trim()
        addLog('parent-to-child', `父組件發送: ${messageToChild.value}`)
        messageToChild.value = ''
        updateCommunicationStats()
    }
}

const updateChildData = () => {
    sharedData.value.counter++
    sharedData.value.items.push(`新項目${sharedData.value.counter}`)
    addLog('parent-action', '父組件更新了共享數據')
    updateCommunicationStats()
}

const resetChildState = () => {
    sharedData.value = {
        counter: 0,
        items: ['項目1', '項目2', '項目3'],
        settings: {
            theme: 'light',
            language: 'zh-TW'
        }
    }
    parentMessage.value = '狀態已重置'
    addLog('parent-action', '父組件重置了子組件狀態')
    updateCommunicationStats()
}

const toggleChildVisibility = () => {
    showChild.value = !showChild.value
    addLog('parent-action', `父組件${showChild.value ? '顯示' : '隱藏'}了子組件`)
}

const handleChildMessage = (message) => {
    childResponse.value = message
    addLog('child-to-parent', `子組件回應: ${message}`)
    updateCommunicationStats()
}

const handleDataUpdated = (data) => {
    addLog('child-action', `子組件更新數據: ${JSON.stringify(data)}`)
    updateCommunicationStats()
}

const handleStatusChanged = (status) => {
    addLog('child-status', `子組件狀態變更: ${status}`)
    updateCommunicationStats()
}

const handleTaskCompleted = (taskName) => {
    emit('task-completed', taskName)
    addLog('task', `任務完成: ${taskName}`)
}

const updateCommunicationStats = () => {
    communicationCount.value++
    lastCommunicationTime.value = new Date().toLocaleTimeString('zh-TW')
}

const addLog = (type, message) => {
    const typeMap = {
        'parent-to-child': '父→子',
        'child-to-parent': '子→父',
        'parent-action': '父操作',
        'child-action': '子操作',
        'child-status': '子狀態',
        'task': '任務'
    }

    communicationLog.value.unshift({
        type,
        typeText: typeMap[type],
        message,
        time: new Date().toLocaleTimeString('zh-TW')
    })

    // 限制日誌條數
    if (communicationLog.value.length > 50) {
        communicationLog.value = communicationLog.value.slice(0, 50)
    }
}

const clearLog = () => {
    communicationLog.value = []
    addLog('parent-action', '清空了通信日誌')
}

const exportLog = () => {
    const logText = communicationLog.value
        .map(log => `[${log.time}] ${log.typeText}: ${log.message}`)
        .join('\n')

    const blob = new Blob([logText], { type: 'text/plain' })
    const url = URL.createObjectURL(blob)
    const a = document.createElement('a')
    a.href = url
    a.download = `communication-log-${new Date().toISOString().slice(0, 10)}.txt`
    a.click()
    URL.revokeObjectURL(url)

    addLog('parent-action', '導出了通信日誌')
}

// 組件掛載時初始化
onMounted(() => {
    addLog('parent-action', '父組件已掛載，開始通信演示')
    emit('task-completed', 'componentComposition')
})
</script>

<style scoped>
.parent-component {
    background: white;
    border-radius: 12px;
    padding: 25px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    border: 1px solid #e9ecef;
}

.demo-header {
    text-align: center;
    margin-bottom: 25px;
    padding-bottom: 15px;
    border-bottom: 2px solid #f1f3f4;
}

.demo-header h4 {
    margin: 0 0 8px 0;
    color: #2c3e50;
    font-size: 1.3em;
}

.demo-header p {
    margin: 0;
    color: #6c757d;
    font-size: 0.9em;
}

.communication-panel {
    background: #f8f9fa;
    border-radius: 10px;
    padding: 20px;
    margin-bottom: 25px;
}

.communication-panel h5 {
    margin: 0 0 15px 0;
    color: #495057;
}

.status-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 15px;
}

.status-item {
    background: white;
    padding: 15px;
    border-radius: 8px;
    border: 1px solid #dee2e6;
}

.status-label {
    display: block;
    font-weight: 600;
    color: #495057;
    margin-bottom: 5px;
    font-size: 0.9em;
}

.status-value {
    color: #007bff;
    font-weight: 500;
}

.control-panel {
    background: #e3f2fd;
    border-radius: 10px;
    padding: 20px;
    margin-bottom: 25px;
}

.control-panel h5 {
    margin: 0 0 15px 0;
    color: #1976d2;
}

.control-actions {
    display: grid;
    gap: 20px;
}

.input-group label {
    display: block;
    margin-bottom: 8px;
    font-weight: 600;
    color: #495057;
}

.input-with-button {
    display: flex;
    gap: 10px;
}

.message-input {
    flex: 1;
    padding: 10px 15px;
    border: 2px solid #dee2e6;
    border-radius: 8px;
    font-size: 14px;
}

.message-input:focus {
    outline: none;
    border-color: #007bff;
}

.send-btn {
    padding: 10px 20px;
    background: #007bff;
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-weight: 600;
    transition: all 0.3s ease;
}

.send-btn:hover {
    background: #0056b3;
    transform: translateY(-2px);
}

.button-group {
    display: flex;
    gap: 15px;
    flex-wrap: wrap;
}

.control-btn {
    padding: 10px 16px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-size: 14px;
    font-weight: 600;
    transition: all 0.3s ease;
}

.update-btn {
    background: #28a745;
    color: white;
}

.update-btn:hover {
    background: #218838;
}

.reset-btn {
    background: #ffc107;
    color: #333;
}

.reset-btn:hover {
    background: #e0a800;
}

.toggle-btn {
    background: #6c757d;
    color: white;
}

.toggle-btn:hover {
    background: #5a6268;
}

.child-area {
    background: #fff3cd;
    border-radius: 10px;
    padding: 20px;
    margin-bottom: 25px;
    border: 2px solid #ffeaa7;
}

.child-area h5 {
    margin: 0 0 15px 0;
    color: #856404;
}

.communication-log {
    background: #f8f9fa;
    border-radius: 10px;
    padding: 20px;
}

.communication-log h5 {
    margin: 0 0 15px 0;
    color: #495057;
}

.log-controls {
    display: flex;
    gap: 10px;
    margin-bottom: 15px;
}

.clear-btn,
.export-btn {
    padding: 8px 16px;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-size: 0.85em;
    font-weight: 600;
    transition: all 0.3s ease;
}

.clear-btn {
    background: #dc3545;
    color: white;
}

.clear-btn:hover {
    background: #c82333;
}

.export-btn {
    background: #17a2b8;
    color: white;
}

.export-btn:hover {
    background: #138496;
}

.log-container {
    max-height: 300px;
    overflow-y: auto;
    border: 1px solid #dee2e6;
    border-radius: 8px;
    background: white;
}

.log-entry {
    display: grid;
    grid-template-columns: auto auto 1fr;
    gap: 15px;
    padding: 10px 15px;
    border-bottom: 1px solid #f1f3f4;
    align-items: center;
    font-size: 0.85em;
}

.log-entry:last-child {
    border-bottom: none;
}

.log-entry.parent-to-child {
    background: #e3f2fd;
}

.log-entry.child-to-parent {
    background: #f3e5f5;
}

.log-entry.parent-action {
    background: #e8f5e8;
}

.log-entry.child-action {
    background: #fff3e0;
}

.log-entry.child-status {
    background: #fce4ec;
}

.log-entry.task {
    background: #f1f8e9;
}

.log-time {
    color: #6c757d;
    font-family: monospace;
    font-size: 0.8em;
}

.log-type {
    padding: 2px 8px;
    border-radius: 12px;
    font-weight: 600;
    font-size: 0.75em;
    background: #495057;
    color: white;
    text-align: center;
    min-width: 50px;
}

.log-message {
    color: #495057;
}

.empty-log {
    padding: 40px;
    text-align: center;
    color: #6c757d;
    font-style: italic;
}

@media (max-width: 768px) {
    .status-grid {
        grid-template-columns: 1fr;
    }

    .input-with-button {
        flex-direction: column;
    }

    .button-group {
        flex-direction: column;
    }

    .log-controls {
        flex-direction: column;
    }

    .log-entry {
        grid-template-columns: 1fr;
        gap: 5px;
    }
}
</style>
