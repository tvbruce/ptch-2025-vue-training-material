<template>
    <div class="answering-area">
        <h2>🎯 實作練習區 - Watcher 觀察者</h2>
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

// 模擬搜尋資料
// eslint-disable-next-line no-unused-vars
const mockSearchData = ref([
    { id: 1, title: 'Vue.js 教程', description: '學習 Vue.js 框架的完整指南', score: 95 },
    { id: 2, title: 'JavaScript 基礎', description: 'JavaScript 程式設計基礎知識', score: 88 },
    { id: 3, title: 'React 入門', description: 'React 框架入門教程', score: 82 },
    { id: 4, title: 'CSS 進階', description: '進階 CSS 技巧和最佳實踐', score: 76 },
    { id: 5, title: 'Node.js 後端', description: 'Node.js 後端開發教程', score: 90 }
])

// 🎯 任務：實作 calculationResult 計算屬性
const calculationResult = computed(() => {
    // 請在這裡實作計算邏輯
    // 根據 num1, operator, num2 計算結果
    return 0
})

// 🎯 任務：實作 addWatchLog 方法
// eslint-disable-next-line no-unused-vars
const addWatchLog = (field, oldValue, newValue) => {
    // 請在這裡實作新增監聽日誌的邏輯
    console.log('請實作新增監聽日誌功能')
}

// 🎯 任務：實作 clearWatchLogs 方法
const clearWatchLogs = () => {
    // 請在這裡實作清空監聽日誌的邏輯
    console.log('請實作清空監聽日誌功能')
}

// 🎯 任務：實作 addSkill 方法
const addSkill = () => {
    // 請在這裡實作新增技能的邏輯
    console.log('請實作新增技能功能')
}

// 🎯 任務：實作 removeSkill 方法
// eslint-disable-next-line no-unused-vars
const removeSkill = (index) => {
    // 請在這裡實作移除技能的邏輯
    console.log('請實作移除技能功能')
}

// 🎯 任務：實作 clearHistory 方法
const clearHistory = () => {
    // 請在這裡實作清空計算歷史的邏輯
    console.log('請實作清空歷史功能')
}

// 🎯 任務：實作 performSearch 方法
// eslint-disable-next-line no-unused-vars
const performSearch = async (keyword) => {
    // 請在這裡實作執行搜尋的邏輯
    // 1. 設定搜尋狀態
    // 2. 模擬 API 調用
    // 3. 更新搜尋結果
    // 4. 記錄搜尋統計
    console.log('請實作搜尋功能')
}

// 🎯 任務：實作基本資料監聽
// eslint-disable-next-line no-unused-vars
watch(userName, (newValue, oldValue) => {
    // 請在這裡實作用戶名稱變化監聽
    console.log('請實作用戶名稱監聽')
})

// eslint-disable-next-line no-unused-vars
watch(userAge, (newValue, oldValue) => {
    // 請在這裡實作用戶年齡變化監聽
    console.log('請實作用戶年齡監聽')
})

// eslint-disable-next-line no-unused-vars
watch(userEmail, (newValue, oldValue) => {
    // 請在這裡實作用戶郵箱變化監聽
    console.log('請實作用戶郵箱監聽')
})

// 🎯 任務：實作深度對象監聽
// eslint-disable-next-line no-unused-vars
watch(userProfile, (newValue, oldValue) => {
    // 請在這裡實作用戶資料深度監聽
    // 使用 deep: true 選項
    console.log('請實作深度對象監聽')
}, { deep: true })

// 🎯 任務：實作計算結果監聽
// eslint-disable-next-line no-unused-vars
watch(calculationResult, (newValue, oldValue) => {
    // 請在這裡實作計算結果變化監聽
    // 將計算記錄加入歷史
    console.log('請實作計算結果監聽')
})

// 🎯 任務：實作搜尋關鍵字監聽
// eslint-disable-next-line no-unused-vars
watch(searchKeyword, (newValue, oldValue) => {
    // 請在這裡實作搜尋關鍵字變化監聽
    // 使用防抖機制避免頻繁搜尋
    console.log('請實作搜尋關鍵字監聽')
})

// 🎯 任務：實作 watchEffect
watchEffect(() => {
    // 請在這裡實作 watchEffect
    // 自動追蹤 num1, num2, operator 的變化
    console.log('請實作 watchEffect')
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
}

.log-entry {
    display: grid;
    grid-template-columns: 80px 100px 1fr 20px 1fr;
    gap: 0.5rem;
    padding: 0.25rem 0;
    border-bottom: 1px solid #f1f3f4;
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
}

.history-item {
    display: grid;
    grid-template-columns: 1fr auto auto;
    gap: 1rem;
    padding: 0.5rem 0;
    border-bottom: 1px solid #f1f3f4;
    font-family: monospace;
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
}
</style>
