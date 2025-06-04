<template>
    <div class="data-monitor-practice">
        <h2>👀 數據監控練習 - Watcher 觀察者</h2>
        <p class="route-info">📍 路徑：/WatcherSamples/DataMonitorPractice.vue</p>
        <p class="description">
            📝 <strong>練習目標：</strong>學習 Vue 3 watch 和 watchEffect 的使用，掌握數據變化監聽
        </p>

        <div class="demo-section">
            <h3>🎯 練習任務</h3>
            <div class="task-list">
                <div class="task-item">
                    <span>✅ 1. 基本 watch 監聽器</span>
                </div>
                <div class="task-item">
                    <span>✅ 2. 深度監聽對象變化</span>
                </div>
                <div class="task-item">
                    <span>✅ 3. watchEffect 自動追蹤</span>
                </div>
                <div class="task-item">
                    <span>✅ 4. 監聽多個數據源</span>
                </div>
                <div class="task-item">
                    <span>✅ 5. 條件監聽與停止監聽</span>
                </div>
            </div>
        </div>

        <!-- 用戶資料監控 -->
        <div class="demo-section">
            <h3>👤 用戶資料監控</h3>
            <div class="monitor-container">
                <div class="input-panel">
                    <h4>修改用戶資料</h4>
                    <div class="form-group">
                        <label>姓名:</label>
                        <input v-model="user.name" class="input-field">
                    </div>
                    <div class="form-group">
                        <label>年齡:</label>
                        <input v-model.number="user.age" type="number" class="input-field">
                    </div>
                    <div class="form-group">
                        <label>電子郵件:</label>
                        <input v-model="user.email" type="email" class="input-field">
                    </div>
                    <div class="form-group">
                        <label>城市:</label>
                        <select v-model="user.address.city" class="select-field">
                            <option value="taipei">台北</option>
                            <option value="taichung">台中</option>
                            <option value="kaohsiung">高雄</option>
                            <option value="tainan">台南</option>
                        </select>
                    </div>
                    <div class="form-group">
                        <label>國家:</label>
                        <input v-model="user.address.country" class="input-field">
                    </div>
                </div>

                <div class="monitor-panel">
                    <h4>監聽日誌</h4>
                    <div class="log-container">
                        <div v-for="(log, index) in watchLogs" :key="index" class="log-entry"
                            :class="getLogTypeClass(log.type)">
                            <span class="log-time">{{ log.time }}</span>
                            <span class="log-type">{{ log.type }}</span>
                            <span class="log-message">{{ log.message }}</span>
                        </div>
                    </div>
                    <button @click="clearLogs" class="btn btn-secondary btn-sm">
                        清空日誌
                    </button>
                </div>
            </div>
        </div>

        <!-- 購物車監控 -->
        <div class="demo-section">
            <h3>🛒 購物車監控</h3>
            <div class="cart-monitor">
                <div class="cart-controls">
                    <h4>購物車操作</h4>
                    <div class="product-selector">
                        <select v-model="selectedProduct" class="select-field">
                            <option value="">選擇商品</option>
                            <option v-for="product in products" :key="product.id" :value="product">
                                {{ product.name }} - ${{ product.price }}
                            </option>
                        </select>
                        <button @click="addToCart" :disabled="!selectedProduct" class="btn btn-primary">
                            加入購物車
                        </button>
                    </div>

                    <div class="cart-items">
                        <div v-for="(item, index) in cart.items" :key="index" class="cart-item">
                            <span>{{ item.name }}</span>
                            <div class="quantity-controls">
                                <button @click="decreaseQuantity(index)" class="btn btn-sm">-</button>
                                <span>{{ item.quantity }}</span>
                                <button @click="increaseQuantity(index)" class="btn btn-sm">+</button>
                            </div>
                            <span>${{ (item.price * item.quantity).toFixed(2) }}</span>
                            <button @click="removeFromCart(index)" class="btn btn-danger btn-sm">刪除</button>
                        </div>
                    </div>

                    <div class="cart-summary">
                        <div class="summary-row">
                            <span>商品總數: {{ cart.totalItems }}</span>
                        </div>
                        <div class="summary-row">
                            <span>總價: ${{ cart.totalPrice.toFixed(2) }}</span>
                        </div>
                        <div class="summary-row">
                            <span>折扣: -${{ cart.discount.toFixed(2) }}</span>
                        </div>
                        <div class="summary-row total">
                            <span>最終金額: ${{ cart.finalPrice.toFixed(2) }}</span>
                        </div>
                    </div>
                </div>

                <div class="cart-analytics">
                    <h4>購物車分析</h4>
                    <div class="analytics-grid">
                        <div class="analytics-card">
                            <div class="card-value">{{ cartAnalytics.averagePrice.toFixed(2) }}</div>
                            <div class="card-label">平均單價</div>
                        </div>
                        <div class="analytics-card">
                            <div class="card-value">{{ cartAnalytics.changeCount }}</div>
                            <div class="card-label">變更次數</div>
                        </div>
                        <div class="analytics-card">
                            <div class="card-value">{{ cartAnalytics.lastChanged }}</div>
                            <div class="card-label">最後變更</div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- 搜索監控 -->
        <div class="demo-section">
            <h3>🔍 搜索監控</h3>
            <div class="search-monitor">
                <div class="search-controls">
                    <input v-model="searchQuery" placeholder="輸入搜索關鍵字..." class="input-field search-input">
                    <div class="search-stats">
                        <span>搜索次數: {{ searchStats.count }}</span>
                        <span>結果數量: {{ searchResults.length }}</span>
                    </div>
                </div>

                <div class="search-results">
                    <div v-for="result in searchResults" :key="result.id" class="search-result">
                        <h5>{{ result.title }}</h5>
                        <p>{{ result.description }}</p>
                        <span class="result-category">{{ result.category }}</span>
                    </div>
                    <div v-if="searchQuery && searchResults.length === 0" class="no-results">
                        沒有找到相關結果
                    </div>
                </div>
            </div>
        </div>

        <!-- 監聽器控制 -->
        <div class="demo-section">
            <h3>⚙️ 監聽器控制</h3>
            <div class="watcher-controls">
                <div class="control-group">
                    <h4>監聽器開關</h4>
                    <label class="checkbox-label">
                        <input v-model="watcherConfig.userWatch" type="checkbox">
                        <span>用戶資料監聽</span>
                    </label>
                    <label class="checkbox-label">
                        <input v-model="watcherConfig.cartWatch" type="checkbox">
                        <span>購物車監聽</span>
                    </label>
                    <label class="checkbox-label">
                        <input v-model="watcherConfig.searchWatch" type="checkbox">
                        <span>搜索監聽</span>
                    </label>
                </div>

                <div class="control-group">
                    <h4>監聽選項</h4>
                    <label class="checkbox-label">
                        <input v-model="watcherConfig.immediate" type="checkbox">
                        <span>立即執行 (immediate)</span>
                    </label>
                    <label class="checkbox-label">
                        <input v-model="watcherConfig.deep" type="checkbox">
                        <span>深度監聽 (deep)</span>
                    </label>
                </div>
            </div>
        </div>

        <div class="code-example">
            <h4>💻 關鍵代碼</h4>
            <pre v-pre><code>import { ref, watch, watchEffect } from 'vue'

// 基本 watch 用法
watch(source, (newValue, oldValue) =&gt; {
  console.log('值改變了:', oldValue, '→', newValue)
})

// 深度監聽對象
watch(user, (newUser, oldUser) =&gt; {
  console.log('用戶資料變更')
}, { deep: true })

// 立即執行
watch(searchQuery, (query) =&gt; {
  performSearch(query)
}, { immediate: true })

// watchEffect 自動追蹤依賴
watchEffect(() =&gt; {
  console.log('購物車總價:', cart.totalPrice)
})

// 監聽多個數據源
watch([user.name, user.email], ([newName, newEmail]) =&gt; {
  updateProfile(newName, newEmail)
})

// 停止監聽
const stopWatcher = watch(data, callback)
stopWatcher() // 停止監聽</code></pre>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, watch, watchEffect, onMounted } from 'vue'

// 用戶資料
const user = ref({
    name: '張三',
    age: 25,
    email: 'zhang@example.com',
    address: {
        city: 'taipei',
        country: '台灣'
    }
})

// 監聽日誌
const watchLogs = ref([])

// 商品數據
const products = [
    { id: 1, name: '筆記型電腦', price: 25000 },
    { id: 2, name: '滑鼠', price: 500 },
    { id: 3, name: '鍵盤', price: 1200 },
    { id: 4, name: '螢幕', price: 8000 },
    { id: 5, name: '耳機', price: 1500 }
]

// 購物車
const cart = ref({
    items: [],
    totalItems: 0,
    totalPrice: 0,
    discount: 0,
    finalPrice: 0
})

const selectedProduct = ref('')

// 購物車分析
const cartAnalytics = ref({
    averagePrice: 0,
    changeCount: 0,
    lastChanged: ''
})

// 搜索
const searchQuery = ref('')
const searchResults = ref([])
const searchStats = ref({ count: 0 })

// 監聽器配置
const watcherConfig = ref({
    userWatch: true,
    cartWatch: true,
    searchWatch: true,
    immediate: false,
    deep: true
})

// 搜索數據
const searchData = [
    { id: 1, title: 'Vue 3 教程', description: '學習 Vue 3 的完整指南', category: '教育' },
    { id: 2, title: 'JavaScript 進階', description: '深入了解 JavaScript 高級特性', category: '編程' },
    { id: 3, title: 'React 基礎', description: 'React 框架入門教程', category: '前端' },
    { id: 4, title: 'Node.js 開發', description: '後端開發與 API 設計', category: '後端' },
    { id: 5, title: 'CSS 動畫', description: '創建美麗的網頁動畫效果', category: '設計' }
]

// 添加日誌
const addLog = (type, message) => {
    watchLogs.value.unshift({
        type,
        message,
        time: new Date().toLocaleTimeString()
    })

    // 限制日誌數量
    if (watchLogs.value.length > 50) {
        watchLogs.value.pop()
    }
}

// 獲取日誌類型樣式
const getLogTypeClass = (type) => {
    const classes = {
        'user': 'log-user',
        'cart': 'log-cart',
        'search': 'log-search',
        'watchEffect': 'log-effect'
    }
    return classes[type] || ''
}

// 清空日誌
const clearLogs = () => {
    watchLogs.value = []
}

// 購物車操作
const addToCart = () => {
    if (!selectedProduct.value) return

    const existingItem = cart.value.items.find(item => item.id === selectedProduct.value.id)

    if (existingItem) {
        existingItem.quantity++
    } else {
        cart.value.items.push({
            ...selectedProduct.value,
            quantity: 1
        })
    }

    selectedProduct.value = ''
    updateCartTotals()
}

const removeFromCart = (index) => {
    cart.value.items.splice(index, 1)
    updateCartTotals()
}

const increaseQuantity = (index) => {
    cart.value.items[index].quantity++
    updateCartTotals()
}

const decreaseQuantity = (index) => {
    if (cart.value.items[index].quantity > 1) {
        cart.value.items[index].quantity--
    } else {
        removeFromCart(index)
    }
    updateCartTotals()
}

const updateCartTotals = () => {
    cart.value.totalItems = cart.value.items.reduce((sum, item) => sum + item.quantity, 0)
    cart.value.totalPrice = cart.value.items.reduce((sum, item) => sum + (item.price * item.quantity), 0)

    // 計算折扣 (滿1000折50)
    cart.value.discount = cart.value.totalPrice >= 1000 ? 50 : 0
    cart.value.finalPrice = cart.value.totalPrice - cart.value.discount
}

// 執行搜索
const performSearch = (query) => {
    if (!query.trim()) {
        searchResults.value = []
        return
    }

    searchStats.value.count++

    searchResults.value = searchData.filter(item =>
        item.title.toLowerCase().includes(query.toLowerCase()) ||
        item.description.toLowerCase().includes(query.toLowerCase()) ||
        item.category.toLowerCase().includes(query.toLowerCase())
    )
}

// 監聽器設置
let userWatcher = null
let cartWatcher = null
let searchWatcher = null

const setupWatchers = () => {
    // 用戶資料監聽
    if (watcherConfig.value.userWatch) {
        userWatcher = watch(
            user,
            (newUser) => {
                addLog('user', `用戶資料變更: ${JSON.stringify(newUser)}`)
            },
            {
                deep: watcherConfig.value.deep,
                immediate: watcherConfig.value.immediate
            }
        )

        // 單獨監聽姓名變更
        watch(
            () => user.value.name,
            (newName, oldName) => {
                if (oldName && newName !== oldName) {
                    addLog('user', `姓名變更: ${oldName} → ${newName}`)
                }
            }
        )

        // 監聽年齡變更
        watch(
            () => user.value.age,
            (newAge, oldAge) => {
                if (oldAge && newAge !== oldAge) {
                    addLog('user', `年齡變更: ${oldAge} → ${newAge}`)
                }
            }
        )
    }

    // 購物車監聽
    if (watcherConfig.value.cartWatch) {
        cartWatcher = watch(
            () => cart.value.items,
            (newItems) => {
                cartAnalytics.value.changeCount++
                cartAnalytics.value.lastChanged = new Date().toLocaleTimeString()

                if (newItems.length > 0) {
                    cartAnalytics.value.averagePrice = cart.value.totalPrice / cart.value.totalItems
                } else {
                    cartAnalytics.value.averagePrice = 0
                }

                addLog('cart', `購物車變更: ${newItems.length} 項商品`)
            },
            { deep: true }
        )
    }

    // 搜索監聽
    if (watcherConfig.value.searchWatch) {
        searchWatcher = watch(
            searchQuery,
            (newQuery, oldQuery) => {
                if (newQuery !== oldQuery) {
                    addLog('search', `搜索查詢: "${newQuery}"`)
                    performSearch(newQuery)
                }
            },
            { immediate: watcherConfig.value.immediate }
        )
    }
}

const stopWatchers = () => {
    if (userWatcher) userWatcher()
    if (cartWatcher) cartWatcher()
    if (searchWatcher) searchWatcher()
}

// watchEffect 示例
watchEffect(() => {
    if (cart.value.totalPrice > 0) {
        addLog('watchEffect', `購物車總價更新: $${cart.value.totalPrice.toFixed(2)}`)
    }
})

watchEffect(() => {
    if (searchResults.value.length > 0) {
        addLog('watchEffect', `搜索結果更新: 找到 ${searchResults.value.length} 個結果`)
    }
})

// 監聽監聽器配置變更
watch(
    watcherConfig,
    () => {
        stopWatchers()
        setupWatchers()
    },
    { deep: true }
)

// 初始化
onMounted(() => {
    setupWatchers()
})
</script>

<style scoped>
.monitor-container {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
    margin: 1rem 0;
}

.input-panel,
.monitor-panel {
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
    color: #555;
}

.log-container {
    max-height: 300px;
    overflow-y: auto;
    background: #2c3e50;
    color: #ecf0f1;
    padding: 1rem;
    border-radius: 8px;
    font-family: 'Courier New', monospace;
    font-size: 0.9rem;
    margin-bottom: 1rem;
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
    min-width: 100px;
    font-weight: bold;
}

.log-user .log-type {
    color: #3498db;
}

.log-cart .log-type {
    color: #2ecc71;
}

.log-search .log-type {
    color: #f39c12;
}

.log-effect .log-type {
    color: #e74c3c;
}

.log-message {
    flex: 1;
}

.cart-monitor {
    display: grid;
    grid-template-columns: 1fr 300px;
    gap: 2rem;
}

.cart-controls {
    background: white;
    padding: 1.5rem;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.product-selector {
    display: flex;
    gap: 1rem;
    margin-bottom: 1.5rem;
}

.cart-item {
    display: flex;
    align-items: center;
    gap: 1rem;
    padding: 0.75rem;
    border: 1px solid #ddd;
    border-radius: 4px;
    margin-bottom: 0.5rem;
}

.quantity-controls {
    display: flex;
    align-items: center;
    gap: 0.5rem;
}

.cart-summary {
    border-top: 2px solid #ddd;
    padding-top: 1rem;
    margin-top: 1rem;
}

.summary-row {
    display: flex;
    justify-content: space-between;
    padding: 0.25rem 0;
}

.summary-row.total {
    font-weight: bold;
    font-size: 1.1rem;
    color: #2ecc71;
}

.cart-analytics {
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

.analytics-card {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 1rem;
    border-radius: 8px;
    text-align: center;
}

.card-value {
    font-size: 1.5rem;
    font-weight: bold;
    margin-bottom: 0.5rem;
}

.card-label {
    font-size: 0.9rem;
    opacity: 0.9;
}

.search-monitor {
    background: white;
    padding: 1.5rem;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.search-input {
    width: 100%;
    margin-bottom: 1rem;
}

.search-stats {
    display: flex;
    gap: 2rem;
    margin-bottom: 1rem;
    font-size: 0.9rem;
    color: #666;
}

.search-results {
    max-height: 300px;
    overflow-y: auto;
}

.search-result {
    border: 1px solid #ddd;
    border-radius: 4px;
    padding: 1rem;
    margin-bottom: 0.5rem;
}

.search-result h5 {
    margin: 0 0 0.5rem 0;
    color: #3498db;
}

.search-result p {
    margin: 0 0 0.5rem 0;
    color: #666;
}

.result-category {
    background: #f8f9fa;
    padding: 0.25rem 0.5rem;
    border-radius: 4px;
    font-size: 0.8rem;
    color: #666;
}

.no-results {
    text-align: center;
    color: #666;
    font-style: italic;
    padding: 2rem;
}

.watcher-controls {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
    background: white;
    padding: 1.5rem;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.control-group h4 {
    margin-bottom: 1rem;
    color: #2c3e50;
}

.checkbox-label {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    margin-bottom: 0.5rem;
    cursor: pointer;
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
    .monitor-container {
        grid-template-columns: 1fr;
    }

    .cart-monitor {
        grid-template-columns: 1fr;
    }

    .watcher-controls {
        grid-template-columns: 1fr;
    }

    .product-selector {
        flex-direction: column;
    }
}
</style>
