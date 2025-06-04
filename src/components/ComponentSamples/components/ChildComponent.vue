<template>
    <div class="child-component">
        <div class="child-header">
            <h5>👶 子組件</h5>
            <div class="status-indicator" :class="{ active: isActive }">
                {{ isActive ? '🟢 活躍' : '🔴 停用' }}
            </div>
        </div>

        <!-- 接收到的父組件消息 -->
        <div class="message-display">
            <h6>📨 來自父組件的消息</h6>
            <div class="message-content">
                {{ parentMessage }}
            </div>
            <button @click="respondToParent" class="respond-btn">
                💬 回應父組件
            </button>
        </div>

        <!-- 共享數據操作 -->
        <div class="data-section">
            <h6>📊 共享數據操作</h6>
            <div class="data-display">
                <div class="data-item">
                    <span class="data-label">計數器:</span>
                    <span class="data-value">{{ sharedData.counter }}</span>
                    <button @click="incrementCounter" class="data-btn">➕</button>
                </div>

                <div class="data-item">
                    <span class="data-label">項目列表:</span>
                    <div class="items-list">
                        <div v-for="(item, index) in sharedData.items" :key="index" class="item-tag">
                            {{ item }}
                            <button @click="removeItem(index)" class="remove-btn">✕</button>
                        </div>
                    </div>
                </div>

                <div class="add-item-section">
                    <input v-model="newItem" type="text" placeholder="添加新項目..." class="item-input"
                        @keyup.enter="addItem" />
                    <button @click="addItem" class="add-btn">➕ 添加</button>
                </div>
            </div>
        </div>

        <!-- 配置面板 -->
        <div class="config-section">
            <h6>⚙️ 組件配置</h6>
            <div class="config-display">
                <div class="config-item">
                    <span class="config-label">允許編輯:</span>
                    <span class="config-value" :class="{ enabled: config.allowEdit }">
                        {{ config.allowEdit ? '✅ 是' : '❌ 否' }}
                    </span>
                </div>
                <div class="config-item">
                    <span class="config-label">最大項目數:</span>
                    <span class="config-value">{{ config.maxItems }}</span>
                </div>
                <div class="config-item">
                    <span class="config-label">自動保存:</span>
                    <span class="config-value" :class="{ enabled: config.autoSave }">
                        {{ config.autoSave ? '✅ 開啟' : '❌ 關閉' }}
                    </span>
                </div>
            </div>
        </div>

        <!-- 子組件操作面板 -->
        <div class="action-panel">
            <h6>🎮 子組件操作</h6>
            <div class="action-buttons">
                <button @click="sendRandomMessage" class="action-btn message-btn">
                    🎲 發送隨機消息
                </button>
                <button @click="toggleStatus" class="action-btn status-btn">
                    🔄 切換狀態
                </button>
                <button @click="simulateError" class="action-btn error-btn">
                    ⚠️ 模擬錯誤
                </button>
                <button @click="performComplexAction" class="action-btn complex-btn">
                    🚀 複雜操作
                </button>
            </div>
        </div>

        <!-- 子組件內部狀態 -->
        <div class="internal-state">
            <h6>🔍 內部狀態</h6>
            <div class="state-grid">
                <div class="state-item">
                    <span class="state-label">內部計數:</span>
                    <span class="state-value">{{ internalCounter }}</span>
                </div>
                <div class="state-item">
                    <span class="state-label">操作次數:</span>
                    <span class="state-value">{{ actionCount }}</span>
                </div>
                <div class="state-item">
                    <span class="state-label">最後操作:</span>
                    <span class="state-value">{{ lastAction }}</span>
                </div>
                <div class="state-item">
                    <span class="state-label">組件ID:</span>
                    <span class="state-value">{{ componentId }}</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue'

// 定義 Props
const props = defineProps({
    parentMessage: {
        type: String,
        default: '無消息'
    },
    sharedData: {
        type: Object,
        default: () => ({
            counter: 0,
            items: [],
            settings: {}
        })
    },
    config: {
        type: Object,
        default: () => ({
            allowEdit: true,
            maxItems: 10,
            autoSave: false
        })
    }
})

// 定義事件發射
const emit = defineEmits(['child-message', 'data-updated', 'status-changed', 'task-completed'])

// 響應式數據
const isActive = ref(true)
const newItem = ref('')
const internalCounter = ref(0)
const actionCount = ref(0)
const lastAction = ref('無操作')
const componentId = ref('')

// 隨機消息列表
const randomMessages = [
    '子組件運行正常！',
    '數據同步成功！',
    '準備接收新指令',
    '狀態更新完成',
    '等待父組件響應',
    '執行任務中...',
    '組件初始化完成',
    '數據驗證通過'
]

// 方法
const respondToParent = () => {
    const responses = [
        '收到父組件消息！',
        '子組件已處理完成',
        '感謝父組件的指示',
        '子組件狀態良好',
        '準備執行下一步操作'
    ]
    const response = responses[Math.floor(Math.random() * responses.length)]
    emit('child-message', response)
    updateActionStats('回應父組件')
}

const incrementCounter = () => {
    if (props.config.allowEdit) {
        const newData = { ...props.sharedData, counter: props.sharedData.counter + 1 }
        emit('data-updated', { type: 'counter', value: newData.counter })
        updateActionStats('增加計數器')
    } else {
        alert('編輯功能已禁用')
    }
}

const addItem = () => {
    if (!newItem.value.trim()) return

    if (props.sharedData.items.length >= props.config.maxItems) {
        alert(`最多只能添加 ${props.config.maxItems} 個項目`)
        return
    }

    if (props.config.allowEdit) {
        const newItems = [...props.sharedData.items, newItem.value.trim()]
        emit('data-updated', { type: 'items', value: newItems })
        newItem.value = ''
        updateActionStats('添加項目')
    } else {
        alert('編輯功能已禁用')
    }
}

const removeItem = (index) => {
    if (props.config.allowEdit) {
        const newItems = props.sharedData.items.filter((_, i) => i !== index)
        emit('data-updated', { type: 'items', value: newItems })
        updateActionStats('刪除項目')
    } else {
        alert('編輯功能已禁用')
    }
}

const sendRandomMessage = () => {
    const message = randomMessages[Math.floor(Math.random() * randomMessages.length)]
    emit('child-message', message)
    updateActionStats('發送隨機消息')
}

const toggleStatus = () => {
    isActive.value = !isActive.value
    emit('status-changed', isActive.value ? '活躍' : '停用')
    updateActionStats('切換狀態')
}

const simulateError = () => {
    emit('child-message', '⚠️ 子組件發生模擬錯誤！')
    emit('status-changed', '錯誤狀態')
    updateActionStats('模擬錯誤')
}

const performComplexAction = () => {
    // 模擬複雜操作
    internalCounter.value += 5

    const complexData = {
        timestamp: new Date().toISOString(),
        operation: 'complex-action',
        result: Math.random() * 100
    }

    emit('data-updated', { type: 'complex', value: complexData })
    emit('child-message', '🚀 複雜操作執行完成！')
    updateActionStats('執行複雜操作')
}

const updateActionStats = (action) => {
    actionCount.value++
    lastAction.value = action
    internalCounter.value++
}

const generateComponentId = () => {
    return 'child-' + Math.random().toString(36).substr(2, 9)
}

// 監聽父組件消息變化
watch(() => props.parentMessage, (newMessage) => {
    if (newMessage && newMessage !== '歡迎使用組件通信演示！') {
        updateActionStats('接收父組件消息')
    }
})

// 組件掛載時初始化
onMounted(() => {
    componentId.value = generateComponentId()
    emit('child-message', '子組件已掛載並準備就緒')
    emit('status-changed', '已初始化')
    emit('task-completed', 'propsUsage')
    emit('task-completed', 'eventEmit')
    updateActionStats('組件掛載')
})
</script>

<style scoped>
.child-component {
    background: #fff8e1;
    border-radius: 10px;
    padding: 20px;
    border: 2px solid #ffcc02;
}

.child-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
    padding-bottom: 10px;
    border-bottom: 1px solid #ffcc02;
}

.child-header h5 {
    margin: 0;
    color: #f57f17;
}

.status-indicator {
    padding: 4px 12px;
    border-radius: 20px;
    font-size: 0.8em;
    font-weight: 600;
    background: #ffcdd2;
    color: #c62828;
}

.status-indicator.active {
    background: #c8e6c9;
    color: #2e7d32;
}

.message-display,
.data-section,
.config-section,
.action-panel,
.internal-state {
    background: white;
    border-radius: 8px;
    padding: 15px;
    margin-bottom: 15px;
    border: 1px solid #ffcc02;
}

.message-display h6,
.data-section h6,
.config-section h6,
.action-panel h6,
.internal-state h6 {
    margin: 0 0 12px 0;
    color: #f57f17;
    font-size: 1em;
}

.message-content {
    background: #f5f5f5;
    padding: 12px;
    border-radius: 6px;
    margin-bottom: 10px;
    border-left: 4px solid #ffcc02;
    font-style: italic;
}

.respond-btn {
    background: #ff9800;
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 6px;
    cursor: pointer;
    font-size: 0.85em;
    font-weight: 600;
    transition: all 0.3s ease;
}

.respond-btn:hover {
    background: #f57c00;
    transform: translateY(-1px);
}

.data-display {
    display: grid;
    gap: 12px;
}

.data-item {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 8px;
    background: #f9f9f9;
    border-radius: 6px;
}

.data-label {
    font-weight: 600;
    color: #424242;
    min-width: 80px;
}

.data-value {
    color: #1976d2;
    font-weight: 500;
}

.data-btn {
    background: #4caf50;
    color: white;
    border: none;
    padding: 4px 8px;
    border-radius: 4px;
    cursor: pointer;
    font-size: 0.8em;
}

.data-btn:hover {
    background: #388e3c;
}

.items-list {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
    flex: 1;
}

.item-tag {
    background: #e3f2fd;
    color: #1976d2;
    padding: 4px 8px;
    border-radius: 12px;
    font-size: 0.8em;
    display: flex;
    align-items: center;
    gap: 4px;
}

.remove-btn {
    background: #f44336;
    color: white;
    border: none;
    border-radius: 50%;
    width: 16px;
    height: 16px;
    cursor: pointer;
    font-size: 0.7em;
    display: flex;
    align-items: center;
    justify-content: center;
}

.add-item-section {
    display: flex;
    gap: 8px;
    align-items: center;
}

.item-input {
    flex: 1;
    padding: 8px 12px;
    border: 1px solid #ddd;
    border-radius: 6px;
    font-size: 0.85em;
}

.add-btn {
    background: #2196f3;
    color: white;
    border: none;
    padding: 8px 12px;
    border-radius: 6px;
    cursor: pointer;
    font-size: 0.85em;
    font-weight: 600;
}

.add-btn:hover {
    background: #1976d2;
}

.config-display {
    display: grid;
    gap: 8px;
}

.config-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 6px 0;
}

.config-label {
    font-weight: 600;
    color: #424242;
}

.config-value {
    color: #f44336;
}

.config-value.enabled {
    color: #4caf50;
}

.action-buttons {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
    gap: 10px;
}

.action-btn {
    padding: 10px 12px;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-size: 0.8em;
    font-weight: 600;
    transition: all 0.3s ease;
}

.message-btn {
    background: #9c27b0;
    color: white;
}

.message-btn:hover {
    background: #7b1fa2;
}

.status-btn {
    background: #ff5722;
    color: white;
}

.status-btn:hover {
    background: #d84315;
}

.error-btn {
    background: #f44336;
    color: white;
}

.error-btn:hover {
    background: #d32f2f;
}

.complex-btn {
    background: #3f51b5;
    color: white;
}

.complex-btn:hover {
    background: #303f9f;
}

.state-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 10px;
}

.state-item {
    background: #f5f5f5;
    padding: 10px;
    border-radius: 6px;
    text-align: center;
}

.state-label {
    display: block;
    font-size: 0.8em;
    color: #666;
    margin-bottom: 4px;
}

.state-value {
    font-weight: 600;
    color: #1976d2;
    font-size: 0.9em;
}

@media (max-width: 768px) {
    .child-header {
        flex-direction: column;
        gap: 10px;
        text-align: center;
    }

    .data-item {
        flex-direction: column;
        align-items: stretch;
        text-align: center;
    }

    .add-item-section {
        flex-direction: column;
    }

    .action-buttons {
        grid-template-columns: 1fr;
    }

    .state-grid {
        grid-template-columns: 1fr;
    }
}
</style>
