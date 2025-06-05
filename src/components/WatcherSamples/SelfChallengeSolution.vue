<template>
    <div class="self-challenge-solution">
        <h2>🎯 自我試煉解答 - Watcher 觀察者</h2>
        <p class="route-info">📍 路徑：/WatcherSamples/SelfChallengeSolution.vue</p>

        <div class="watcher-container">
            <h3>📊 數據監控系統</h3>

            <!-- 用戶資料編輯區 -->
            <div class="user-editor">
                <h4>👤 用戶資料編輯</h4>

                <div class="form-grid">
                    <div class="form-group">
                        <label for="userName">姓名:</label>
                        <input id="userName" v-model="user.name" type="text" placeholder="輸入姓名">
                    </div>

                    <div class="form-group">
                        <label for="userAge">年齡:</label>
                        <input id="userAge" v-model.number="user.age" type="number" min="1" max="120">
                    </div>

                    <div class="form-group">
                        <label for="activityLevel">活躍度 (%):</label>
                        <input id="activityLevel" v-model.number="user.activityLevel" type="range" min="0" max="100">
                        <span class="range-value">{{ user.activityLevel }}%</span>
                    </div>

                    <div class="form-group">
                        <label>興趣愛好:</label>
                        <div class="hobby-controls">
                            <input v-model="newHobby" type="text" placeholder="新增興趣" @keyup.enter="addHobby">
                            <button @click="addHobby" class="add-btn">新增</button>
                        </div>
                        <div class="hobby-list">
                            <span v-for="(hobby, index) in user.hobbies" :key="index" class="hobby-tag"
                                @click="removeHobby(index)">
                                {{ hobby }} ✕
                            </span>
                        </div>
                    </div>
                </div>
            </div>

            <!-- 監聽器控制面板 -->
            <div class="watcher-controls">
                <h4>⚙️ 監聽器控制</h4>

                <div class="control-grid">
                    <label class="control-item">
                        <input type="checkbox" v-model="watchSettings.enableNameWatch" @change="toggleWatchers">
                        <span>監控姓名變化</span>
                    </label>

                    <label class="control-item">
                        <input type="checkbox" v-model="watchSettings.enableDeepWatch" @change="toggleWatchers">
                        <span>深度監控用戶資料</span>
                    </label>

                    <label class="control-item">
                        <input type="checkbox" v-model="watchSettings.enableActivityWatch" @change="toggleWatchers">
                        <span>監控活躍度變化</span>
                    </label>
                </div>

                <div class="action-buttons">
                    <button @click="stopAllWatchers" class="btn stop-btn">
                        🛑 停止所有監聽器
                    </button>
                    <button @click="clearLogs" class="btn clear-btn">
                        🗑️ 清空日誌
                    </button>
                </div>
            </div>

            <!-- 用戶等級顯示 -->
            <div class="user-level">
                <h4>🏆 用戶等級</h4>
                <div class="level-display" :class="`level-${userLevel.toLowerCase()}`">
                    <div class="level-badge">{{ userLevel }}</div>
                    <div class="level-info">
                        <div>年齡: {{ user.age }}歲 ({{ getAgeGroup() }})</div>
                        <div>活躍度: {{ user.activityLevel }}% ({{ getActivityGroup() }})</div>
                    </div>
                </div>
            </div>

            <!-- 統計面板 -->
            <div class="stats-panel">
                <h4>📈 監控統計</h4>
                <div class="stats-grid">
                    <div class="stat-item">
                        <div class="stat-value">{{ totalChanges }}</div>
                        <div class="stat-label">總變化次數</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value">{{ logs.length }}</div>
                        <div class="stat-label">日誌條數</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value">{{ watchers.length }}</div>
                        <div class="stat-label">活躍監聽器</div>
                    </div>
                    <div class="stat-item">
                        <div class="stat-value">{{ user.hobbies.length }}</div>
                        <div class="stat-label">興趣數量</div>
                    </div>
                </div>
            </div>

            <!-- 監控日誌 -->
            <div class="logs-panel">
                <h4>📝 監控日誌</h4>
                <div class="log-filters">
                    <button v-for="type in logTypes" :key="type" @click="filterLogType = type" class="filter-btn"
                        :class="{ active: filterLogType === type }">
                        {{ getLogTypeLabel(type) }}
                    </button>
                </div>

                <div class="logs-list">
                    <div v-for="(log, index) in filteredLogs" :key="index" class="log-item" :class="`log-${log.type}`">
                        <span class="log-time">{{ log.time }}</span>
                        <span class="log-type">{{ getLogTypeIcon(log.type) }}</span>
                        <span class="log-message">{{ log.message }}</span>
                    </div>
                    <div v-if="filteredLogs.length === 0" class="no-logs">
                        {{ filterLogType === 'all' ? '暫無日誌記錄' : `暫無 ${getLogTypeLabel(filterLogType)} 類型的日誌` }}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, reactive, computed, watch, watchEffect, onMounted } from 'vue'

// 響應式數據
const user = reactive({
    name: '張小明',
    age: 25,
    activityLevel: 60,
    hobbies: ['閱讀', '音樂']
})

const watchSettings = reactive({
    enableNameWatch: true,
    enableDeepWatch: true,
    enableActivityWatch: true
})

const logs = ref([])
const totalChanges = ref(0)
const watchers = ref([])
const newHobby = ref('')
const filterLogType = ref('all')

// 日誌類型
const logTypes = ['all', 'watch', 'watchEffect', 'deep', 'activity', 'multiple']

// 1. userLevel (computed) - 計算用戶等級邏輯
const userLevel = computed(() => {
    const age = user.age
    const activity = user.activityLevel

    // 年齡分段
    let ageGroup
    if (age < 18) ageGroup = 'Youth'
    else if (age <= 30) ageGroup = 'Adult'
    else if (age <= 50) ageGroup = 'Senior'
    else ageGroup = 'Elder'

    // 活躍度等級
    let activityGroup
    if (activity <= 25) activityGroup = 'Low'
    else if (activity <= 50) activityGroup = 'Medium'
    else if (activity <= 75) activityGroup = 'High'
    else activityGroup = 'VeryHigh'

    // 等級計算
    if (ageGroup === 'Youth' && (activityGroup === 'Low' || activityGroup === 'Medium')) return 'Bronze'
    if (ageGroup === 'Adult' && activityGroup === 'Low') return 'Bronze'
    if (ageGroup === 'Adult' && (activityGroup === 'Medium' || activityGroup === 'High')) return 'Silver'
    if (ageGroup === 'Senior' && (activityGroup === 'Low' || activityGroup === 'Medium')) return 'Silver'
    if (ageGroup === 'Senior' && activityGroup === 'High') return 'Gold'
    if (ageGroup === 'Elder' && (activityGroup === 'Medium' || activityGroup === 'High')) return 'Gold'
    if (ageGroup === 'Adult' && activityGroup === 'VeryHigh') return 'Gold'
    if (ageGroup === 'Elder' && activityGroup === 'VeryHigh') return 'Platinum'
    if (ageGroup === 'Senior' && activityGroup === 'VeryHigh') return 'Platinum'

    return 'Bronze'
})

// 2. addLog(type, message) - 實作添加日誌的輔助函數
const addLog = (type, message) => {
    logs.value.push({
        time: new Date().toLocaleTimeString(),
        type,
        message
    })
    totalChanges.value += 1
}

// 3. watchUserName() - 使用 watch 監控 user.name 的變化
const watchUserName = () => {
    if (!watchSettings.enableNameWatch) return null

    const stopWatcher = watch(
        () => user.name,
        (newValue, oldValue) => {
            if (oldValue !== undefined) {
                addLog('watch', `用戶名從 "${oldValue}" 變更為 "${newValue}"`)
            }
        },
        { immediate: false }
    )

    return stopWatcher
}

// 4. watchUserDeep() - 使用 watch 深度監控整個 user 對象
const watchUserDeep = () => {
    if (!watchSettings.enableDeepWatch) return null

    const stopWatcher = watch(
        user,
        () => {
            addLog('deep', `用戶資料發生深度變化 (等級: ${userLevel.value})`)
        },
        { deep: true, immediate: false }
    )

    return stopWatcher
}

// 5. watchActivityLevel() - 監控 user.activityLevel 的變化
const watchActivityLevel = () => {
    if (!watchSettings.enableActivityWatch) return null

    const stopWatcher = watch(
        () => user.activityLevel,
        (newValue) => {
            let message
            if (newValue >= 80) {
                message = `🔥 用戶活躍度極高！(${newValue}%)`
            } else if (newValue >= 60) {
                message = `⚡ 用戶活躍度良好 (${newValue}%)`
            } else if (newValue < 30) {
                message = `😴 用戶活躍度偏低 (${newValue}%)`
            } else {
                message = `📊 活躍度變更為 ${newValue}%`
            }
            addLog('activity', message)
        },
        { immediate: true }
    )

    return stopWatcher
}

// 6. setupWatchEffect() - 使用 watchEffect 自動追蹤用戶數據變化
const setupWatchEffect = () => {
    const stopWatcher = watchEffect(() => {
        const message = `🤖 watchEffect: ${user.name}(${user.age}歲) 活躍度${user.activityLevel}% 興趣${user.hobbies.length}項`
        addLog('watchEffect', message)
    })

    return stopWatcher
}

// 7. watchMultipleSources() - 同時監控用戶名和年齡的變化
const watchMultipleSources = () => {
    const stopWatcher = watch(
        [() => user.name, () => user.age],
        ([newName, newAge], [oldName, oldAge]) => {
            if (oldName !== undefined && oldAge !== undefined) {
                let messages = []
                if (newName !== oldName) {
                    messages.push(`👤 用戶名: ${oldName} → ${newName}`)
                }
                if (newAge !== oldAge) {
                    messages.push(`🎂 年齡: ${oldAge} → ${newAge}`)
                }
                if (messages.length > 0) {
                    addLog('multiple', messages.join(', '))
                }
            }
        },
        { immediate: false }
    )

    return stopWatcher
}

// 設置所有監聽器
const setupWatchers = () => {
    stopAllWatchers()

    const nameWatcher = watchUserName()
    const deepWatcher = watchUserDeep()
    const activityWatcher = watchActivityLevel()
    const effectWatcher = setupWatchEffect()
    const multipleWatcher = watchMultipleSources()

    watchers.value = [nameWatcher, deepWatcher, activityWatcher, effectWatcher, multipleWatcher].filter(Boolean)
}

// 切換監聽器
const toggleWatchers = () => {
    setupWatchers()
}

// 停止所有監聽器
const stopAllWatchers = () => {
    watchers.value.forEach(stop => stop && stop())
    watchers.value = []
}

// 清空日誌
const clearLogs = () => {
    logs.value = []
    totalChanges.value = 0
}

// 興趣管理
const addHobby = () => {
    if (newHobby.value.trim() && !user.hobbies.includes(newHobby.value.trim())) {
        user.hobbies.push(newHobby.value.trim())
        newHobby.value = ''
    }
}

const removeHobby = (index) => {
    user.hobbies.splice(index, 1)
}

// 輔助函數
const getAgeGroup = () => {
    const age = user.age
    if (age < 18) return '青少年'
    if (age <= 30) return '青年'
    if (age <= 50) return '中年'
    return '長者'
}

const getActivityGroup = () => {
    const activity = user.activityLevel
    if (activity <= 25) return '低'
    if (activity <= 50) return '中'
    if (activity <= 75) return '高'
    return '極高'
}

const getLogTypeLabel = (type) => {
    const labels = {
        'all': '全部',
        'watch': 'Watch',
        'watchEffect': 'WatchEffect',
        'deep': '深度監控',
        'activity': '活躍度',
        'multiple': '多源監控'
    }
    return labels[type] || type
}

const getLogTypeIcon = (type) => {
    const icons = {
        'watch': '👁️',
        'watchEffect': '🤖',
        'deep': '🔍',
        'activity': '📊',
        'multiple': '🔗'
    }
    return icons[type] || '📝'
}

// 過濾日誌
const filteredLogs = computed(() => {
    if (filterLogType.value === 'all') {
        return logs.value.slice().reverse()
    }
    return logs.value.filter(log => log.type === filterLogType.value).slice().reverse()
})

// 組件掛載時設置監聽器
onMounted(() => {
    setupWatchers()
})
</script>

<style scoped>
.self-challenge-solution {
    max-width: 1200px;
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

.watcher-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
    align-items: start;
}

.user-editor,
.watcher-controls,
.user-level,
.stats-panel {
    background: white;
    padding: 20px;
    border-radius: 15px;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
    border: 1px solid #e1e5e9;
}

.user-editor h4,
.watcher-controls h4,
.user-level h4,
.stats-panel h4 {
    color: #2c3e50;
    margin-bottom: 15px;
    text-align: center;
}

.form-grid {
    display: grid;
    gap: 15px;
}

.form-group {
    display: flex;
    flex-direction: column;
}

.form-group label {
    font-weight: 600;
    color: #2c3e50;
    margin-bottom: 5px;
}

.form-group input {
    padding: 10px;
    border: 2px solid #e1e5e9;
    border-radius: 8px;
    font-size: 14px;
    transition: border-color 0.3s ease;
}

.form-group input:focus {
    outline: none;
    border-color: #3498db;
}

.range-value {
    margin-top: 5px;
    font-weight: 600;
    color: #3498db;
}

.hobby-controls {
    display: flex;
    gap: 10px;
    margin-bottom: 10px;
}

.add-btn {
    padding: 10px 15px;
    background: #3498db;
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: background 0.3s ease;
}

.add-btn:hover {
    background: #2980b9;
}

.hobby-list {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
}

.hobby-tag {
    background: #e3f2fd;
    color: #1976d2;
    padding: 5px 10px;
    border-radius: 15px;
    font-size: 12px;
    cursor: pointer;
    transition: all 0.3s ease;
}

.hobby-tag:hover {
    background: #bbdefb;
    transform: scale(1.05);
}

.control-grid {
    display: grid;
    gap: 10px;
    margin-bottom: 15px;
}

.control-item {
    display: flex;
    align-items: center;
    cursor: pointer;
    padding: 10px;
    background: #f8f9fa;
    border-radius: 8px;
    transition: background 0.3s ease;
}

.control-item:hover {
    background: #e9ecef;
}

.control-item input {
    margin-right: 10px;
}

.action-buttons {
    display: flex;
    gap: 10px;
}

.btn {
    flex: 1;
    padding: 10px;
    border: none;
    border-radius: 8px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
}

.stop-btn {
    background: #e74c3c;
    color: white;
}

.stop-btn:hover {
    background: #c0392b;
}

.clear-btn {
    background: #95a5a6;
    color: white;
}

.clear-btn:hover {
    background: #7f8c8d;
}

.level-display {
    text-align: center;
    padding: 20px;
    border-radius: 10px;
    transition: all 0.3s ease;
}

.level-bronze {
    background: linear-gradient(135deg, #cd7f32, #b8860b);
    color: white;
}

.level-silver {
    background: linear-gradient(135deg, #c0c0c0, #a8a8a8);
    color: white;
}

.level-gold {
    background: linear-gradient(135deg, #ffd700, #ffb347);
    color: #2c3e50;
}

.level-platinum {
    background: linear-gradient(135deg, #e5e4e2, #b8b8b8);
    color: #2c3e50;
}

.level-badge {
    font-size: 2rem;
    font-weight: bold;
    margin-bottom: 10px;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
}

.level-info {
    font-size: 0.9rem;
    opacity: 0.9;
}

.stats-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
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
    font-size: 1.5rem;
    font-weight: bold;
    color: #2c3e50;
    margin-bottom: 5px;
}

.stat-label {
    font-size: 0.8rem;
    color: #7f8c8d;
}

.logs-panel {
    grid-column: 1 / -1;
    background: white;
    padding: 20px;
    border-radius: 15px;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
    border: 1px solid #e1e5e9;
}

.logs-panel h4 {
    color: #2c3e50;
    margin-bottom: 15px;
    text-align: center;
}

.log-filters {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 15px;
}

.filter-btn {
    padding: 8px 15px;
    border: 2px solid #e1e5e9;
    background: white;
    border-radius: 20px;
    cursor: pointer;
    transition: all 0.3s ease;
    font-size: 12px;
}

.filter-btn:hover {
    border-color: #3498db;
}

.filter-btn.active {
    background: #3498db;
    color: white;
    border-color: #3498db;
}

.logs-list {
    max-height: 400px;
    overflow-y: auto;
}

.log-item {
    display: flex;
    align-items: center;
    padding: 10px;
    margin-bottom: 8px;
    background: #f8f9fa;
    border-radius: 8px;
    border-left: 4px solid #3498db;
    transition: all 0.3s ease;
}

.log-item:hover {
    background: #e9ecef;
    transform: translateX(5px);
}

.log-watch {
    border-left-color: #3498db;
}

.log-watchEffect {
    border-left-color: #9b59b6;
}

.log-deep {
    border-left-color: #e67e22;
}

.log-activity {
    border-left-color: #2ecc71;
}

.log-multiple {
    border-left-color: #e74c3c;
}

.log-time {
    font-family: monospace;
    font-size: 0.8rem;
    color: #7f8c8d;
    margin-right: 10px;
    min-width: 80px;
}

.log-type {
    margin-right: 10px;
    font-size: 1.2rem;
}

.log-message {
    flex: 1;
    color: #2c3e50;
}

.no-logs {
    text-align: center;
    color: #7f8c8d;
    font-style: italic;
    padding: 20px;
}

@media (max-width: 768px) {
    .watcher-container {
        grid-template-columns: 1fr;
    }

    .stats-grid {
        grid-template-columns: 1fr;
    }

    .action-buttons {
        flex-direction: column;
    }

    .log-filters {
        justify-content: center;
    }
}
</style>
