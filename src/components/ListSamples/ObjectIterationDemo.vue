<template>
    <div class="list-rendering-demo">
        <h2>v-for 遍歷物件</h2>
        <p class="route-info">📍 路徑：/ListSamples/ObjectIterationDemo.vue</p>
        <p class="description">
            展示如何使用 v-for 遍歷物件屬性，包含 value、key 和 index 的使用
        </p>

        <!-- 基本物件遍歷 -->
        <div class="demo-section">
            <h3>基本物件遍歷 <span class="code-path">ObjectIterationDemo.vue</span></h3>
            <div class="demo-container">
                <div class="demo-panel">
                    <h4>使用者資訊展示</h4>
                    <div class="result">
                        <div class="user-profile">
                            <div v-for="(value, key) in userInfo" :key="key" class="profile-item">
                                <span class="profile-key">{{ key }}：</span>
                                <span class="profile-value">{{ value }}</span>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="demo-panel">
                    <h4>包含索引的遍歷</h4>
                    <div class="result">
                        <div class="indexed-list">
                            <div v-for="(value, key, index) in userInfo" :key="key" class="indexed-item">
                                <span class="item-index">[{{ index }}]</span>
                                <span class="item-content">{{ key }}: {{ value }}</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <div class="code-example">
                <pre v-pre><code><!-- 只獲取值 -->
&lt;div v-for="value in userInfo" :key="value"&gt;
  {{ value }}
&lt;/div&gt;

<!-- 獲取值和鍵 -->
&lt;div v-for="(value, key) in userInfo" :key="key"&gt;
  {{ key }}: {{ value }}
&lt;/div&gt;

<!-- 獲取值、鍵和索引 -->
&lt;div v-for="(value, key, index) in userInfo" :key="key"&gt;
  [{{ index }}] {{ key }}: {{ value }}
&lt;/div&gt;</code></pre>
            </div>
        </div>

        <!-- 設定頁面範例 -->
        <div class="demo-section">
            <h3>實際應用：設定頁面 <span class="code-path">ObjectIterationDemo.vue</span></h3>
            <div class="demo-container">
                <div class="demo-panel">
                    <h4>系統設定</h4>
                    <div class="controls">
                        <button @click="toggleAllSettings" class="btn btn-primary">
                            {{ allEnabled ? '全部關閉' : '全部開啟' }}
                        </button>
                        <button @click="resetSettings" class="btn btn-secondary">重置設定</button>
                    </div>

                    <div class="result">
                        <div class="settings-list">
                            <div v-for="(setting, key) in systemSettings" :key="key" class="setting-item">
                                <div class="setting-info">
                                    <span class="setting-name">{{ setting.name }}</span>
                                    <span class="setting-desc">{{ setting.description }}</span>
                                </div>
                                <label class="setting-toggle">
                                    <input type="checkbox" v-model="setting.enabled"
                                        @change="onSettingChange(key, setting.enabled)">
                                    <span class="toggle-slider"></span>
                                </label>
                            </div>
                        </div>
                    </div>
                </div>

                <div class="demo-panel">
                    <h4>設定摘要</h4>
                    <div class="result">
                        <div class="settings-summary">
                            <div class="summary-header">
                                已啟用設定 ({{ enabledCount }}/{{ totalCount }})
                            </div>
                            <div class="enabled-settings">
                                <div v-for="(setting, key) in enabledSettings" :key="key" class="enabled-item">
                                    ✅ {{ setting.name }}
                                </div>
                                <div v-if="enabledCount === 0" class="no-settings">
                                    未啟用任何設定
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <div class="code-example">
                <pre v-pre><code>// 遍歷物件並過濾
const enabledSettings = computed(() => {
  const enabled = {}
  for (const [key, setting] of Object.entries(systemSettings.value)) {
    if (setting.enabled) {
      enabled[key] = setting
    }
  }
  return enabled
})

// 模板中使用
&lt;div v-for="(setting, key) in enabledSettings" :key="key"&gt;
  ✅ {{ setting.name }}
&lt;/div&gt;</code></pre>
            </div>
        </div>

        <!-- 動態物件操作 -->
        <div class="demo-section">
            <h3>動態物件操作 <span class="code-path">ObjectIterationDemo.vue</span></h3>
            <div class="demo-container">
                <div class="demo-panel">
                    <h4>購物車商品分類</h4>
                    <div class="controls">
                        <select v-model="selectedCategory" class="input-field">
                            <option value="">選擇分類</option>
                            <option value="電子產品">電子產品</option>
                            <option value="服飾">服飾</option>
                            <option value="食品">食品</option>
                        </select>
                        <input v-model="newProductName" placeholder="商品名稱" class="input-field">
                        <input v-model.number="newProductPrice" type="number" placeholder="價格" class="input-field">
                        <button @click="addProduct" class="btn btn-success">新增商品</button>
                        <button @click="clearCategory" class="btn btn-warning">清空選中分類</button>
                    </div>

                    <div class="result">
                        <div class="category-list">
                            <div v-for="(products, category) in productsByCategory" :key="category"
                                class="category-group">
                                <div class="category-header">
                                    <h5>{{ category }} ({{ products.length }} 項)</h5>
                                    <span class="category-total">總計：${{ getCategoryTotal(products) }}</span>
                                </div>
                                <div class="products-grid">
                                    <div v-for="product in products" :key="product.id" class="product-card">
                                        <span class="product-name">{{ product.name }}</span>
                                        <span class="product-price">${{ product.price }}</span>
                                        <button @click="removeProduct(category, product.id)"
                                            class="btn-remove">✕</button>
                                    </div>
                                </div>
                            </div>
                            <div v-if="Object.keys(productsByCategory).length === 0" class="empty-state">
                                購物車是空的
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <div class="code-example">
                <pre v-pre><code>// 動態分組物件
const productsByCategory = ref({
  '電子產品': [
    { id: 1, name: '手機', price: 15000 },
    { id: 2, name: '筆電', price: 30000 }
  ],
  '服飾': [
    { id: 3, name: 'T恤', price: 500 }
  ]
})

// 新增到動態物件
const addProduct = () => {
  if (!productsByCategory.value[selectedCategory.value]) {
    productsByCategory.value[selectedCategory.value] = []
  }
  productsByCategory.value[selectedCategory.value].push(newProduct)
}</code></pre>
            </div>
        </div>

        <!-- 說明區塊 -->
        <div class="info-box">
            <h4>💡 物件遍歷要點</h4>
            <ul>
                <li><code>v-for="value in object"</code> - 只獲取屬性值</li>
                <li><code>v-for="(value, key) in object"</code> - 獲取值和鍵</li>
                <li><code>v-for="(value, key, index) in object"</code> - 獲取值、鍵和索引</li>
                <li>物件屬性的遍歷順序在現代瀏覽器中是可預測的</li>
                <li>使用 <code>key</code> 作為 <code>:key</code> 屬性通常是最佳選擇</li>
                <li>可以結合 computed 屬性來處理複雜的物件操作</li>
            </ul>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 基本物件遍歷
const userInfo = ref({
    姓名: '張小明',
    年齡: 28,
    職業: '前端工程師',
    城市: '台北',
    email: 'zhang@example.com'
})

// 系統設定
const systemSettings = ref({
    notifications: {
        name: '推播通知',
        description: '接收應用程式通知',
        enabled: true
    },
    darkMode: {
        name: '深色模式',
        description: '使用深色主題界面',
        enabled: false
    },
    autoSave: {
        name: '自動儲存',
        description: '自動儲存您的工作',
        enabled: true
    },
    analytics: {
        name: '數據分析',
        description: '分享使用數據以改善服務',
        enabled: false
    }
})

// 商品分類
const productsByCategory = ref({
    '電子產品': [
        { id: 1, name: '智慧型手機', price: 15000 },
        { id: 2, name: '筆記型電腦', price: 30000 }
    ],
    '服飾': [
        { id: 3, name: '休閒T恤', price: 500 },
        { id: 4, name: '牛仔褲', price: 1200 }
    ],
    '食品': [
        { id: 5, name: '有機蘋果', price: 150 }
    ]
})

// 新增商品的表單
const selectedCategory = ref('')
const newProductName = ref('')
const newProductPrice = ref('')
let productIdCounter = 6

// 計算屬性
const enabledSettings = computed(() => {
    const enabled = {}
    for (const [key, setting] of Object.entries(systemSettings.value)) {
        if (setting.enabled) {
            enabled[key] = setting
        }
    }
    return enabled
})

const enabledCount = computed(() => Object.keys(enabledSettings.value).length)
const totalCount = computed(() => Object.keys(systemSettings.value).length)
const allEnabled = computed(() => enabledCount.value === totalCount.value)

// 方法
const onSettingChange = (key, enabled) => {
    console.log(`設定 ${key} 已${enabled ? '啟用' : '停用'}`)
}

const toggleAllSettings = () => {
    const targetState = !allEnabled.value
    Object.values(systemSettings.value).forEach(setting => {
        setting.enabled = targetState
    })
}

const resetSettings = () => {
    systemSettings.value = {
        notifications: { name: '推播通知', description: '接收應用程式通知', enabled: true },
        darkMode: { name: '深色模式', description: '使用深色主題界面', enabled: false },
        autoSave: { name: '自動儲存', description: '自動儲存您的工作', enabled: true },
        analytics: { name: '數據分析', description: '分享使用數據以改善服務', enabled: false }
    }
}

const addProduct = () => {
    if (!selectedCategory.value || !newProductName.value || !newProductPrice.value) {
        alert('請填寫完整的商品資訊')
        return
    }

    if (!productsByCategory.value[selectedCategory.value]) {
        productsByCategory.value[selectedCategory.value] = []
    }

    productsByCategory.value[selectedCategory.value].push({
        id: productIdCounter++,
        name: newProductName.value,
        price: newProductPrice.value
    })

    // 清空表單
    newProductName.value = ''
    newProductPrice.value = ''
}

const removeProduct = (category, productId) => {
    const products = productsByCategory.value[category]
    const index = products.findIndex(p => p.id === productId)
    if (index > -1) {
        products.splice(index, 1)

        // 如果分類下沒有商品了，刪除分類
        if (products.length === 0) {
            delete productsByCategory.value[category]
        }
    }
}

const clearCategory = () => {
    if (selectedCategory.value && productsByCategory.value[selectedCategory.value]) {
        delete productsByCategory.value[selectedCategory.value]
        selectedCategory.value = ''
    }
}

const getCategoryTotal = (products) => {
    return products.reduce((total, product) => total + product.price, 0)
}
</script>

<style scoped>
/* 組件樣式已在全域 main.css 中定義 */
</style>
