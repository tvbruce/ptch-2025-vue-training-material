<template>
    <div class="answering-area">
        <h2>🎯 實作練習區 - Computed 計算屬性</h2>
        <p class="description">
            📝 <strong>任務：</strong>建立商品篩選系統，實作各種計算屬性功能
        </p>

        <!-- 任務一：篩選條件 -->
        <div class="task-section">
            <h3>🔍 任務一：篩選條件</h3>
            <div class="filters">
                <div class="filter-group">
                    <label>🔎 搜尋商品：</label>
                    <input v-model="searchKeyword" placeholder="輸入商品名稱..." class="form-input">
                </div>

                <div class="filter-group">
                    <label>📂 商品分類：</label>
                    <select v-model="selectedCategory" class="form-select">
                        <option value="">全部分類</option>
                        <option value="電子產品">電子產品</option>
                        <option value="服裝">服裝</option>
                        <option value="家具">家具</option>
                        <option value="書籍">書籍</option>
                    </select>
                </div>

                <div class="filter-group">
                    <label>💰 價格範圍：</label>
                    <input v-model.number="minPrice" type="number" placeholder="最低價" class="form-input price-input">
                    <span>-</span>
                    <input v-model.number="maxPrice" type="number" placeholder="最高價" class="form-input price-input">
                </div>

                <div class="filter-group">
                    <label>📊 排序方式：</label>
                    <select v-model="sortBy" class="form-select">
                        <option value="">預設排序</option>
                        <option value="name-asc">名稱升序</option>
                        <option value="name-desc">名稱降序</option>
                        <option value="price-asc">價格升序</option>
                        <option value="price-desc">價格降序</option>
                    </select>
                </div>

                <button @click="resetFilters" class="btn btn-secondary">重置篩選</button>
            </div>
        </div>

        <!-- 任務二：統計資訊 -->
        <div class="task-section">
            <h3>📊 任務二：統計資訊</h3>
            <div class="stats-grid">
                <div class="stat-card">
                    <h4>找到商品</h4>
                    <p class="stat-number">{{ productStats.count }} 件</p>
                </div>
                <div class="stat-card">
                    <h4>平均價格</h4>
                    <p class="stat-number">${{ productStats.averagePrice }}</p>
                </div>
                <div class="stat-card">
                    <h4>最高價格</h4>
                    <p class="stat-number">${{ productStats.maxPrice }}</p>
                </div>
                <div class="stat-card">
                    <h4>最低價格</h4>
                    <p class="stat-number">${{ productStats.minPrice }}</p>
                </div>
            </div>
        </div>

        <!-- 任務三：商品列表 -->
        <div class="task-section">
            <h3>🛍️ 任務三：商品列表</h3>
            <div class="product-list">
                <!-- 🎯 任務：在這裡使用 v-for 渲染 finalProducts -->
                <div v-if="finalProducts.length === 0" class="no-products">
                    <p>沒有找到符合條件的商品</p>
                </div>

                <!--
        <div v-for="product in finalProducts" :key="product.id" class="product-card">
          <h4>{{ product.name }}</h4>
          <span class="category">{{ product.category }}</span>
          <p class="price">${{ product.price }}</p>
        </div>
        -->
            </div>
        </div>

        <!-- 開發提示 -->
        <div class="hint-section">
            <h4>💡 開發提示</h4>
            <ul>
                <li>searchedProducts: 根據 searchKeyword 篩選商品名稱</li>
                <li>filteredProducts: 在搜尋結果基礎上根據 selectedCategory 篩選</li>
                <li>priceFilteredProducts: 在分類篩選基礎上根據價格範圍篩選</li>
                <li>finalProducts: 在價格篩選基礎上根據 sortBy 排序</li>
                <li>productStats: 計算最終結果的統計資訊</li>
            </ul>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 商品資料
const products = ref([
    { id: 1, name: 'iPhone 14', category: '電子產品', price: 25000 },
    { id: 2, name: 'MacBook Pro', category: '電子產品', price: 55000 },
    { id: 3, name: '運動T恤', category: '服裝', price: 299 },
    { id: 4, name: '牛仔褲', category: '服裝', price: 1200 },
    { id: 5, name: '辦公椅', category: '家具', price: 3500 },
    { id: 6, name: '書桌', category: '家具', price: 8000 },
    { id: 7, name: 'Vue.js 教程', category: '書籍', price: 450 },
    { id: 8, name: 'JavaScript 指南', category: '書籍', price: 380 }
])

// 篩選條件
const searchKeyword = ref('')
const selectedCategory = ref('')
const minPrice = ref(0)
const maxPrice = ref(100000)
const sortBy = ref('')

// 🎯 任務：實作 searchedProducts 計算屬性

const searchedProducts = computed(() => {
    // 請在這裡實作關鍵字搜尋邏輯
    // 根據 searchKeyword 篩選商品名稱（不區分大小寫）
    // 如果 searchKeyword 為空，返回所有商品
    return products.value
})

// 🎯 任務：實作 filteredProducts 計算屬性

const filteredProducts = computed(() => {
    // 請在這裡實作分類篩選邏輯
    // 在 searchedProducts 基礎上根據 selectedCategory 篩選
    // 如果 selectedCategory 為空，返回所有搜尋結果
    return searchedProducts.value
})

// 🎯 任務：實作 priceFilteredProducts 計算屬性

const priceFilteredProducts = computed(() => {
    // 請在這裡實作價格範圍篩選邏輯
    // 在 filteredProducts 基礎上根據 minPrice 和 maxPrice 篩選
    return filteredProducts.value
})

// 🎯 任務：實作 finalProducts 計算屬性（排序）

const finalProducts = computed(() => {
    // 請在這裡實作排序邏輯
    // 在 priceFilteredProducts 基礎上根據 sortBy 排序
    // 支援：name-asc, name-desc, price-asc, price-desc
    return priceFilteredProducts.value
})

// 🎯 任務：實作 productStats 計算屬性
const productStats = computed(() => {
    // 請在這裡實作統計資訊計算
    // 包含：count, averagePrice, maxPrice, minPrice
    // eslint-disable-next-line no-unused-vars
    const productsData = finalProducts.value
    return {
        count: 0,
        averagePrice: 0,
        maxPrice: 0,
        minPrice: 0
    }
})

// 🎯 任務：實作 resetFilters 方法
const resetFilters = () => {
    // 請在這裡實作重置篩選條件的邏輯
    // 將所有篩選條件重置為初始值
    console.log('請實作重置篩選功能')
}
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
    border-left: 4px solid #28a745;
}

.filters {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1rem;
    margin-bottom: 1rem;
}

.filter-group {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}

.filter-group label {
    font-weight: bold;
    color: #495057;
}

.form-input,
.form-select {
    padding: 0.5rem;
    border: 1px solid #ddd;
    border-radius: 4px;
}

.price-input {
    max-width: 120px;
}

.btn {
    padding: 0.5rem 1rem;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    align-self: flex-start;
}

.btn-secondary {
    background: #6c757d;
    color: white;
}

.stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
}

.stat-card {
    background: white;
    padding: 1.5rem;
    border-radius: 8px;
    text-align: center;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.stat-number {
    font-size: 1.5rem;
    font-weight: bold;
    color: #28a745;
    margin: 0;
}

.product-list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1rem;
}

.product-card {
    background: white;
    padding: 1.5rem;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.category {
    background: #007bff;
    color: white;
    padding: 0.2rem 0.5rem;
    border-radius: 12px;
    font-size: 0.8rem;
}

.price {
    font-size: 1.2rem;
    font-weight: bold;
    color: #28a745;
    margin: 0.5rem 0;
}

.no-products {
    grid-column: 1 / -1;
    text-align: center;
    padding: 2rem;
    color: #6c757d;
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
</style>
