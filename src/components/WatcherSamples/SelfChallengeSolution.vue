<template>
    <div class="answering-area">
        <h2>🎯 參考答案 - Watcher 觀察者</h2>
        <p class="description">
            📝 <strong>任務：</strong>建立一個資料監控系統，實作各種 watch 監聽功能
        </p>

        <!-- 任務一：基本監聽 -->
        <div class="task-section">
            <h3>👁️ 任務一：基本資料監聽</h3>
            <div class="basic-watch-container">
                <div class="input-controls">
                    <div class="form-group">
                        <label>用戶名稱：</label>
                        <input v-model="userName" placeholder="輸入用戶名稱" class="form-input">
                    </div>

                    <div class="form-group">
                        <label>用戶年齡：</label>
                        <input v-model.number="userAge" type="number" placeholder="輸入年齡" class="form-input">
                    </div>

                    <div class="form-group">
                        <label>用戶郵箱：</label>
                        <input v-model="userEmail" type="email" placeholder="輸入郵箱" class="form-input">
                    </div>
                </div>

                <div class="watch-log">
                    <h4>監聽日誌：</h4>
                    <div class="log-container">
                        <div v-for="(log, index) in watchLogs" :key="index" class="log-entry">
                            <span class="log-time">{{ log.time }}</span>
                            <span class="log-field">{{ log.field }}</span>
                            <span class="log-old">{{ log.oldValue }}</span>
                            <span class="log-arrow">→</span>
                            <span class="log-new">{{ log.newValue }}</span>
                        </div>
                    </div>
                    <button @click="clearWatchLogs" class="btn btn-secondary">清空日誌</button>
                </div>
            </div>
        </div>

        <!-- 任務二：深度監聽 -->
        <div class="task-section">
            <h3>🔍 任務二：深度對象監聽</h3>
            <div class="deep-watch-container">
                <div class="object-editor">
                    <h4>編輯用戶資料：</h4>
                    <div class="form-grid">
                        <div class="form-group">
                            <label>姓名：</label>
                            <input v-model="userProfile.name" class="form-input">
                        </div>

                        <div class="form-group">
                            <label>職業：</label>
                            <input v-model="userProfile.job" class="form-input">
                        </div>

                        <div class="form-group">
                            <label>城市：</label>
                            <input v-model="userProfile.address.city" class="form-input">
                        </div>

                        <div class="form-group">
                            <label>國家：</label>
                            <input v-model="userProfile.address.country" class="form-input">
                        </div>
                    </div>

                    <div class="skills-section">
                        <h5>技能列表：</h5>
                        <div class="skills-list">
                            <div v-for="(skill, index) in userProfile.skills" :key="index" class="skill-item">
                                <input v-model="skill.name" placeholder="技能名稱" class="form-input">
                                <input v-model.number="skill.level" type="number" min="1" max="10" placeholder="等級"
                                    class="form-input">
                                <button @click="removeSkill(index)" class="btn btn-danger btn-sm">刪除</button>
                            </div>
                        </div>
                        <button @click="addSkill" class="btn btn-primary">新增技能</button>
                    </div>
                </div>

                <div class="object-preview">
                    <h4>對象狀態：</h4>
                    <pre class="object-display">{{ JSON.stringify(userProfile, null, 2) }}</pre>

                    <div class="change-summary">
                        <h5>變更摘要：</h5>
                        <p>總變更次數：{{ totalChanges }}</p>
                        <p>最後變更時間：{{ lastChangeTime }}</p>
                        <p>最頻繁變更欄位：{{ mostChangedField }}</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- 任務三：計算屬性監聽 -->
        <div class="task-section">
            <h3>🧮 任務三：計算屬性監聽</h3>
            <div class="computed-watch-container">
                <div class="calculator">
                    <h4>計算器：</h4>
                    <div class="calc-inputs">
                        <input v-model.number="num1" type="number" placeholder="數字1" class="form-input">
                        <select v-model="operator" class="form-select">
                            <option value="+">加 (+)</option>
                            <option value="-">減 (-)</option>
                            <option value="*">乘 (×)</option>
                            <option value="/">除 (÷)</option>
                        </select>
                        <input v-model.number="num2" type="number" placeholder="數字2" class="form-input">
                        <span class="result">= {{ calculationResult }}</span>
                    </div>
                </div>

                <div class="calc-history">
                    <h4>計算歷史：</h4>
                    <div class="history-list">
                        <div v-for="(record, index) in calculationHistory" :key="index" class="history-item">
                            <span class="calculation">{{ record.expression }}</span>
                            <span class="result">= {{ record.result }}</span>
                            <span class="time">{{ record.time }}</span>
                        </div>
                    </div>
                    <button @click="clearHistory" class="btn btn-secondary">清空歷史</button>
                </div>
            </div>
        </div>

        <!-- 任務四：異步監聽 -->
        <div class="task-section">
            <h3>⚡ 任務四：異步操作監聽</h3>
            <div class="async-watch-container">
                <div class="search-controls">
                    <div class="form-group">
                        <label>搜尋關鍵字：</label>
                        <input v-model="searchKeyword" placeholder="輸入搜尋關鍵字" class="form-input">
                        <div class="search-status">
                            <span v-if="isSearching" class="status searching">搜尋中...</span>
                            <span v-else-if="searchResults.length > 0" class="status success">
                                找到 {{ searchResults.length }} 個結果
                            </span>
                            <span v-else-if="searchKeyword && !isSearching" class="status empty">無結果</span>
                        </div>
                    </div>
                </div>

                <div class="search-results">
                    <h4>搜尋結果：</h4>
                    <div class="results-list">
                        <div v-for="result in searchResults" :key="result.id" class="result-item">
                            <h5>{{ result.title }}</h5>
                            <p>{{ result.description }}</p>
                            <span class="result-score">相關度：{{ result.score }}%</span>
                        </div>
                    </div>
                </div>

                <div class="search-analytics">
                    <h4>搜尋分析：</h4>
                    <div class="analytics-grid">
                        <div class="metric">
                            <span class="metric-label">搜尋次數：</span>
                            <span class="metric-value">{{ searchCount }}</span>
                        </div>
                        <div class="metric">
                            <span class="metric-label">平均響應時間：</span>
                            <span class="metric-value">{{ averageResponseTime }}ms</span>
                        </div>
                        <div class="metric">
                            <span class="metric-label">最受歡迎關鍵字：</span>
                            <span class="metric-value">{{ mostPopularKeyword }}</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- 開發提示 -->
        <div class="hint-section">
            <h4>💡 開發提示</h4>
            <ul>
                <li>watch(): 基本監聽，可以獲取新值和舊值</li>
                <li>watchEffect(): 自動追蹤依賴，不提供舊值</li>
                <li>deep: true - 深度監聽對象內部變化</li>
                <li>immediate: true - 立即執行一次監聽器</li>
                <li>flush: 'post' - 在 DOM 更新後執行</li>
            </ul>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, watch, watchEffect } from 'vue'

// 基本監聽資料
const userName = ref('')
const userAge = ref(null)
const userEmail = ref('')
const watchLogs = ref([])

// 深度監聽資料
const userProfile = ref({
    name: '',
    job: '',
    address: {
        city: '',
        country: ''
    },
    skills: []
})
const totalChanges = ref(0)
const lastChangeTime = ref('')
const mostChangedField = ref('')
const fieldChangeCount = ref({})

// 計算屬性監聽資料
const num1 = ref(0)
const num2 = ref(0)
const operator = ref('+')
const calculationHistory = ref([])

// 異步監聽資料
const searchKeyword = ref('')
const isSearching = ref(false)
const searchResults = ref([])
const searchCount = ref(0)
const averageResponseTime = ref(0)
const mostPopularKeyword = ref('')
const searchStats = ref({})
const responseTimes = ref([])

// 防抖計時器
let searchTimeout = null

// 模擬搜尋資料
const mockSearchData = ref([
    { id: 1, title: 'Vue.js 教程', description: '學習 Vue.js 框架的完整指南', score: 95 },
    { id: 2, title: 'JavaScript 基礎', description: 'JavaScript 程式設計基礎知識', score: 88 },
    { id: 3, title: 'React 入門', description: 'React 框架入門教程', score: 82 },
    { id: 4, title: 'CSS 進階', description: '進階 CSS 技巧和最佳實踐', score: 76 },
    { id: 5, title: 'Node.js 後端', description: 'Node.js 後端開發教程', score: 90 }
])

// 計算結果
const calculationResult = computed(() => {
    const n1 = Number(num1.value) || 0
    const n2 = Number(num2.value) || 0

    switch (operator.value) {
        case '+':
            return n1 + n2
        case '-':
            return n1 - n2
        case '*':
            return n1 * n2
        case '/':
            return n2 !== 0 ? (n1 / n2).toFixed(2) : '錯誤：除以零'
        default:
            return 0
    }
})

// 新增監聽日誌
const addWatchLog = (field, oldValue, newValue) => {
    const now = new Date()
    const time = now.toLocaleTimeString()

    watchLogs.value.unshift({
        time,
        field,
        oldValue: oldValue === null || oldValue === undefined ? '空' : String(oldValue),
        newValue: newValue === null || newValue === undefined ? '空' : String(newValue)
    })

    // 限制日誌數量
    if (watchLogs.value.length > 50) {
        watchLogs.value.pop()
    }
}

// 清空監聽日誌
const clearWatchLogs = () => {
    watchLogs.value = []
    addWatchLog('系統', '清空日誌', '操作完成')
}

// 新增技能
const addSkill = () => {
    userProfile.value.skills.push({
        name: '',
        level: 1
    })
}

// 移除技能
const removeSkill = (index) => {
    if (confirm('確定要刪除這個技能嗎？')) {
        userProfile.value.skills.splice(index, 1)
    }
}

// 清空計算歷史
const clearHistory = () => {
    calculationHistory.value = []
}

// 執行搜尋
const performSearch = async (keyword) => {
    if (!keyword.trim()) {
        searchResults.value = []
        return
    }

    isSearching.value = true
    const startTime = Date.now()

    try {
        // 模擬 API 延遲
        await new Promise(resolve => setTimeout(resolve, 500))

        // 模擬搜尋
        const query = keyword.toLowerCase()
        const results = mockSearchData.value.filter(item =>
            item.title.toLowerCase().includes(query) ||
            item.description.toLowerCase().includes(query)
        ).map(item => ({
            ...item,
            score: Math.max(50, Math.floor(Math.random() * 50) + 50)
        }))

        searchResults.value = results

        // 記錄統計
        searchCount.value++
        const responseTime = Date.now() - startTime
        responseTimes.value.push(responseTime)

        // 計算平均響應時間
        averageResponseTime.value = Math.round(
            responseTimes.value.reduce((sum, time) => sum + time, 0) / responseTimes.value.length
        )

        // 記錄關鍵字統計
        if (searchStats.value[keyword]) {
            searchStats.value[keyword]++
        } else {
            searchStats.value[keyword] = 1
        }

        // 找出最受歡迎的關鍵字
        mostPopularKeyword.value = Object.keys(searchStats.value).reduce((a, b) =>
            searchStats.value[a] > searchStats.value[b] ? a : b
        ) || ''

    } catch (error) {
        console.error('搜尋失敗:', error)
        searchResults.value = []
    } finally {
        isSearching.value = false
    }
}

// 追蹤字段變更
const trackFieldChange = (fieldName) => {
    if (fieldChangeCount.value[fieldName]) {
        fieldChangeCount.value[fieldName]++
    } else {
        fieldChangeCount.value[fieldName] = 1
    }

    // 更新最頻繁變更字段
    mostChangedField.value = Object.keys(fieldChangeCount.value).reduce((a, b) =>
        fieldChangeCount.value[a] > fieldChangeCount.value[b] ? a : b
    ) || ''

    // 更新總變更次數和時間
    totalChanges.value++
    lastChangeTime.value = new Date().toLocaleTimeString()
}

// 基本資料監聽
watch(userName, (newValue, oldValue) => {
    if (newValue !== oldValue) {
        addWatchLog('用戶名稱', oldValue, newValue)
        trackFieldChange('用戶名稱')
    }
})

watch(userAge, (newValue, oldValue) => {
    if (newValue !== oldValue) {
        addWatchLog('用戶年齡', oldValue, newValue)
        trackFieldChange('用戶年齡')
    }
})

watch(userEmail, (newValue, oldValue) => {
    if (newValue !== oldValue) {
        addWatchLog('用戶郵箱', oldValue, newValue)
        trackFieldChange('用戶郵箱')
    }
})

// 深度對象監聽
watch(userProfile, (newValue, oldValue) => {
    // 深度監聽會在任何嵌套屬性改變時觸發
    const serializedNew = JSON.stringify(newValue)
    const serializedOld = JSON.stringify(oldValue)

    if (serializedNew !== serializedOld) {
        addWatchLog('用戶資料', '對象已變更', '深度監聽觸發')
        trackFieldChange('用戶資料')
    }
}, { deep: true })

// 監聽用戶資料的具體字段
watch(() => userProfile.value.name, (newValue, oldValue) => {
    if (newValue !== oldValue) {
        addWatchLog('資料-姓名', oldValue, newValue)
        trackFieldChange('資料-姓名')
    }
})

watch(() => userProfile.value.job, (newValue, oldValue) => {
    if (newValue !== oldValue) {
        addWatchLog('資料-職業', oldValue, newValue)
        trackFieldChange('資料-職業')
    }
})

watch(() => userProfile.value.address.city, (newValue, oldValue) => {
    if (newValue !== oldValue) {
        addWatchLog('資料-城市', oldValue, newValue)
        trackFieldChange('資料-城市')
    }
})

watch(() => userProfile.value.address.country, (newValue, oldValue) => {
    if (newValue !== oldValue) {
        addWatchLog('資料-國家', oldValue, newValue)
        trackFieldChange('資料-國家')
    }
})

// 計算結果監聽
watch(calculationResult, (newValue, oldValue) => {
    if (newValue !== oldValue && num1.value !== 0 && num2.value !== 0) {
        const expression = `${num1.value} ${operator.value} ${num2.value}`
        const record = {
            expression,
            result: newValue,
            time: new Date().toLocaleTimeString()
        }

        calculationHistory.value.unshift(record)

        // 限制歷史記錄數量
        if (calculationHistory.value.length > 20) {
            calculationHistory.value.pop()
        }

        addWatchLog('計算結果', oldValue, newValue)
        trackFieldChange('計算結果')
    }
})

// 搜尋關鍵字監聽（防抖處理）
watch(searchKeyword, (newValue, oldValue) => {
    if (newValue !== oldValue) {
        addWatchLog('搜尋關鍵字', oldValue, newValue)

        // 清除之前的計時器
        if (searchTimeout) {
            clearTimeout(searchTimeout)
        }

        // 設置新的計時器，500ms 後執行搜尋
        searchTimeout = setTimeout(() => {
            performSearch(newValue)
        }, 500)
    }
})

// watchEffect 示例
watchEffect(() => {
    // 自動追蹤 num1, num2, operator 的變化
    if (num1.value !== 0 || num2.value !== 0) {
        // 這裡可以執行一些副作用操作
        console.log(`watchEffect: ${num1.value} ${operator.value} ${num2.value} = ${calculationResult.value}`)
    }
})

// 監聽技能數量變化
watch(() => userProfile.value.skills.length, (newLength, oldLength) => {
    if (newLength !== oldLength) {
        addWatchLog('技能數量', oldLength, newLength)
        trackFieldChange('技能數量')
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
    border-left: 4px solid #6f42c1;
}

.basic-watch-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
}

.input-controls {
    background: white;
    padding: 1.5rem;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.form-group {
    margin-bottom: 1rem;
}

.form-group label {
    display: block;
    font-weight: bold;
    margin-bottom: 0.5rem;
    color: #495057;
}

.form-input,
.form-select {
    width: 100%;
    padding: 0.75rem;
    border: 2px solid #dee2e6;
    border-radius: 4px;
    font-size: 1rem;
    transition: border-color 0.3s ease;
}

.form-input:focus,
.form-select:focus {
    outline: none;
    border-color: #6f42c1;
}

.watch-log {
    background: white;
    padding: 1.5rem;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.log-container {
    max-height: 300px;
    overflow-y: auto;
    border: 1px solid #e9ecef;
    border-radius: 4px;
    padding: 1rem;
    margin: 1rem 0;
    font-family: monospace;
    font-size: 0.9rem;
    background: #f8f9fa;
}

.log-entry {
    display: grid;
    grid-template-columns: 80px 100px 1fr 20px 1fr;
    gap: 0.5rem;
    padding: 0.25rem 0;
    border-bottom: 1px solid #f1f3f4;
}

.log-entry:last-child {
    border-bottom: none;
}

.log-time {
    color: #6c757d;
}

.log-field {
    color: #007bff;
    font-weight: bold;
}

.log-old {
    color: #dc3545;
}

.log-arrow {
    color: #28a745;
    text-align: center;
}

.log-new {
    color: #28a745;
}

.deep-watch-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
}

.object-editor {
    background: white;
    padding: 1.5rem;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.form-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
    margin-bottom: 2rem;
}

.skills-section {
    border-top: 1px solid #e9ecef;
    padding-top: 1rem;
}

.skills-list {
    margin: 1rem 0;
}

.skill-item {
    display: grid;
    grid-template-columns: 1fr 80px 80px;
    gap: 0.5rem;
    margin-bottom: 0.5rem;
    align-items: center;
}

.object-preview {
    background: white;
    padding: 1.5rem;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.object-display {
    background: #f8f9fa;
    padding: 1rem;
    border-radius: 4px;
    border: 1px solid #dee2e6;
    font-size: 0.875rem;
    max-height: 300px;
    overflow-y: auto;
}

.change-summary {
    margin-top: 1rem;
    padding: 1rem;
    background: #e3f2fd;
    border-radius: 4px;
}

.computed-watch-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
}

.calculator {
    background: white;
    padding: 1.5rem;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.calc-inputs {
    display: grid;
    grid-template-columns: 1fr auto 1fr auto;
    gap: 1rem;
    align-items: center;
}

.result {
    font-size: 1.2rem;
    font-weight: bold;
    color: #28a745;
}

.calc-history {
    background: white;
    padding: 1.5rem;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.history-list {
    max-height: 300px;
    overflow-y: auto;
    border: 1px solid #e9ecef;
    border-radius: 4px;
    padding: 1rem;
    margin: 1rem 0;
    background: #f8f9fa;
}

.history-item {
    display: grid;
    grid-template-columns: 1fr auto auto;
    gap: 1rem;
    padding: 0.5rem 0;
    border-bottom: 1px solid #f1f3f4;
    font-family: monospace;
}

.history-item:last-child {
    border-bottom: none;
}

.async-watch-container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    gap: 2rem;
}

.search-controls {
    background: white;
    padding: 1.5rem;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.search-status {
    margin-top: 0.5rem;
}

.status {
    padding: 0.25rem 0.5rem;
    border-radius: 12px;
    font-size: 0.875rem;
    font-weight: bold;
}

.status.searching {
    background: #fff3cd;
    color: #856404;
}

.status.success {
    background: #d4edda;
    color: #155724;
}

.status.empty {
    background: #f8d7da;
    color: #721c24;
}

.search-results {
    background: white;
    padding: 1.5rem;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.results-list {
    max-height: 400px;
    overflow-y: auto;
}

.result-item {
    padding: 1rem;
    border: 1px solid #e9ecef;
    border-radius: 4px;
    margin-bottom: 1rem;
    transition: transform 0.2s ease;
}

.result-item:hover {
    transform: translateY(-2px);
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.result-item h5 {
    margin: 0 0 0.5rem 0;
    color: #007bff;
}

.result-item p {
    margin: 0 0 0.5rem 0;
    color: #6c757d;
}

.result-score {
    font-size: 0.875rem;
    color: #28a745;
    font-weight: bold;
}

.search-analytics {
    background: white;
    padding: 1.5rem;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.analytics-grid {
    display: flex;
    flex-direction: column;
    gap: 1rem;
}

.metric {
    display: flex;
    justify-content: space-between;
    padding: 0.5rem;
    background: #f8f9fa;
    border-radius: 4px;
}

.metric-label {
    color: #6c757d;
}

.metric-value {
    font-weight: bold;
    color: #495057;
}

.btn {
    padding: 0.5rem 1rem;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 0.9rem;
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

.btn-sm {
    padding: 0.25rem 0.5rem;
    font-size: 0.8rem;
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

@media (max-width: 768px) {

    .basic-watch-container,
    .deep-watch-container,
    .computed-watch-container {
        grid-template-columns: 1fr;
    }

    .async-watch-container {
        grid-template-columns: 1fr;
    }

    .form-grid {
        grid-template-columns: 1fr;
    }

    .calc-inputs {
        grid-template-columns: 1fr;
    }

    .skill-item {
        grid-template-columns: 1fr;
    }

    .log-entry {
        grid-template-columns: 1fr;
        gap: 0.25rem;
    }

    .history-item {
        grid-template-columns: 1fr;
    }
}
</style>
