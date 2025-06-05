<template>
    <div class="solution">
        <h2>✅ 解答 - Computed 計算屬性</h2>
        <p>完整實現商品篩選功能，展示計算屬性的各種用法</p>

        <!-- 篩選控制 -->
        <div class="demo-card">
            <h4>篩選控制</h4>
            <div class="filter-controls">
                <input v-model="searchKeyword" placeholder="搜尋商品名稱..." />

                <select v-model="selectedCategory">
                    <option value="">所有分類</option>
                    <option value="電子產品">電子產品</option>
                    <option value="服飾">服飾</option>
                    <option value="書籍">書籍</option>
                    <option value="家具">家具</option>
                </select>

                <div class="price-range">
                    <label>價格範圍：</label>
                    <input type="number" v-model="minPrice" placeholder="最低價" min="0" />
                    <span>-</span>
                    <input type="number" v-model="maxPrice" placeholder="最高價" min="0" />
                </div>

                <select v-model="sortBy">
                    <option value="">預設排序</option>
                    <option value="name-asc">名稱升序</option>
                    <option value="name-desc">名稱降序</option>
                    <option value="price-asc">價格升序</option>
                    <option value="price-desc">價格降序</option>
                </select>

                <button @click="resetFilters" class="reset-btn">重置篩選</button>
            </div>
        </div>

        <!-- 統計資訊 -->
        <div class="demo-card">
            <h4>統計資訊</h4>
            <div class="stats-grid">
                <div class="stat-item">
                    <span class="stat-label">商品總數</span>
                    <span class="stat-value">{{ productStats.total }}</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">平均價格</span>
                    <span class="stat-value">${{ productStats.averagePrice }}</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">最高價格</span>
                    <span class="stat-value">${{ productStats.maxPrice }}</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">最低價格</span>
                    <span class="stat-value">${{ productStats.minPrice }}</span>
                </div>
            </div>
        </div>

        <!-- 商品列表 -->
        <div class="demo-card">
            <h4>商品列表 ({{ sortedProducts.length }} 項商品)</h4>

            <div v-if="sortedProducts.length === 0" class="empty-state">
                <p>沒有符合條件的商品</p>
            </div>

            <div v-else class="product-grid">
                <div v-for="product in sortedProducts" :key="product.id" class="product-card">
                    <div class="product-image">
                        <img :src="product.image" :alt="product.name" />
                    </div>
                    <div class="product-info">
                        <h5>{{ product.name }}</h5>
                        <p class="product-category">{{ product.category }}</p>
                        <p class="product-price">${{ product.price }}</p>
                        <p class="product-description">{{ product.description }}</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- 分類統計 -->
        <div class="demo-card">
            <h4>分類統計</h4>
            <div class="category-stats">
                <div v-for="(stats, category) in categoryStats" :key="category" class="category-item">
                    <h5>{{ category }}</h5>
                    <p>商品數量：{{ stats.count }}</p>
                    <p>平均價格：${{ stats.averagePrice.toFixed(2) }}</p>
                    <p>價格範圍：${{ stats.minPrice }} - ${{ stats.maxPrice }}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 篩選條件
const searchKeyword = ref('')
const selectedCategory = ref('')
const minPrice = ref(0)
const maxPrice = ref(1000)
const sortBy = ref('')

// 商品資料
const products = ref([
    { id: 1, name: 'iPhone 14', category: '電子產品', price: 999, description: '最新款智慧型手機', image: 'https://via.placeholder.com/150' },
    { id: 2, name: 'MacBook Pro', category: '電子產品', price: 1999, description: '專業筆記型電腦', image: 'https://via.placeholder.com/150' },
    { id: 3, name: '牛仔褲', category: '服飾', price: 89, description: '經典藍色牛仔褲', image: 'https://via.placeholder.com/150' },
    { id: 4, name: 'T恤', category: '服飾', price: 29, description: '純棉舒適T恤', image: 'https://via.placeholder.com/150' },
    { id: 5, name: 'JavaScript 權威指南', category: '書籍', price: 45, description: '程式設計經典書籍', image: 'https://via.placeholder.com/150' },
    { id: 6, name: 'Vue.js 實戰', category: '書籍', price: 35, description: 'Vue.js 開發指南', image: 'https://via.placeholder.com/150' },
    { id: 7, name: '辦公椅', category: '家具', price: 299, description: '人體工學辦公椅', image: 'https://via.placeholder.com/150' },
    { id: 8, name: '書桌', category: '家具', price: 199, description: '簡約風格書桌', image: 'https://via.placeholder.com/150' },
    { id: 9, name: 'iPad Air', category: '電子產品', price: 599, description: '輕薄平板電腦', image: 'https://via.placeholder.com/150' },
    { id: 10, name: '運動鞋', category: '服飾', price: 129, description: '舒適運動鞋', image: 'https://via.placeholder.com/150' }
])

// 1. searchedProducts 計算屬性
const searchedProducts = computed(() => {
    if (!searchKeyword.value.trim()) {
        return products.value
    }

    const keyword = searchKeyword.value.toLowerCase()
    return products.value.filter(product =>
        product.name.toLowerCase().includes(keyword)
    )
})

// 2. filteredProducts 計算屬性
const filteredProducts = computed(() => {
    let filtered = searchedProducts.value

    // 分類篩選
    if (selectedCategory.value) {
        filtered = filtered.filter(product =>
            product.category === selectedCategory.value
        )
    }

    return filtered
})

// 3. priceFilteredProducts 計算屬性
const priceFilteredProducts = computed(() => {
    return filteredProducts.value.filter(product =>
        product.price >= minPrice.value && product.price <= maxPrice.value
    )
})

// 4. productStats 計算屬性
const productStats = computed(() => {
    const products = priceFilteredProducts.value

    if (products.length === 0) {
        return {
            total: 0,
            averagePrice: '0.00',
            maxPrice: '0.00',
            minPrice: '0.00'
        }
    }

    const prices = products.map(p => p.price)
    const total = prices.reduce((sum, price) => sum + price, 0)

    return {
        total: products.length,
        averagePrice: (total / products.length).toFixed(2),
        maxPrice: Math.max(...prices).toFixed(2),
        minPrice: Math.min(...prices).toFixed(2)
    }
})

// 5. sortedProducts 計算屬性
const sortedProducts = computed(() => {
    const products = [...priceFilteredProducts.value]

    if (!sortBy.value) {
        return products
    }

    return products.sort((a, b) => {
        switch (sortBy.value) {
            case 'name-asc':
                return a.name.localeCompare(b.name)
            case 'name-desc':
                return b.name.localeCompare(a.name)
            case 'price-asc':
                return a.price - b.price
            case 'price-desc':
                return b.price - a.price
            default:
                return 0
        }
    })
})

// 額外的計算屬性：分類統計
const categoryStats = computed(() => {
    const stats = {}

    priceFilteredProducts.value.forEach(product => {
        if (!stats[product.category]) {
            stats[product.category] = {
                count: 0,
                total: 0,
                prices: []
            }
        }

        stats[product.category].count++
        stats[product.category].total += product.price
        stats[product.category].prices.push(product.price)
    })

    // 計算每個分類的統計資訊
    Object.keys(stats).forEach(category => {
        const categoryData = stats[category]
        categoryData.averagePrice = categoryData.total / categoryData.count
        categoryData.minPrice = Math.min(...categoryData.prices)
        categoryData.maxPrice = Math.max(...categoryData.prices)
    })

    return stats
})

// 6. resetFilters 函數
const resetFilters = () => {
    searchKeyword.value = ''
    selectedCategory.value = ''
    minPrice.value = 0
    maxPrice.value = 1000
    sortBy.value = ''
}
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

.filter-controls {
    display: flex;
    flex-wrap: wrap;
    gap: 15px;
    align-items: center;
}

.filter-controls input,
.filter-controls select {
    padding: 8px 12px;
    border: 1px solid #ced4da;
    border-radius: 5px;
    font-size: 0.9em;
}

.price-range {
    display: flex;
    align-items: center;
    gap: 8px;
}

.price-range input {
    width: 100px;
}

.reset-btn {
    padding: 8px 16px;
    background: #dc3545;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background 0.2s;
}

.reset-btn:hover {
    background: #c82333;
}

.stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 15px;
}

.stat-item {
    text-align: center;
    padding: 20px;
    background: #f8f9fa;
    border-radius: 8px;
    border-left: 4px solid #007bff;
}

.stat-label {
    display: block;
    color: #6c757d;
    font-size: 0.9em;
    margin-bottom: 8px;
}

.stat-value {
    display: block;
    font-size: 1.5em;
    font-weight: bold;
    color: #495057;
}

.empty-state {
    text-align: center;
    padding: 40px;
    color: #6c757d;
}

.product-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 20px;
}

.product-card {
    border: 1px solid #e9ecef;
    border-radius: 8px;
    overflow: hidden;
    transition: transform 0.2s, box-shadow 0.2s;
}

.product-card:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.product-image {
    height: 150px;
    overflow: hidden;
}

.product-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.product-info {
    padding: 15px;
}

.product-info h5 {
    margin: 0 0 8px 0;
    color: #495057;
    font-size: 1.1em;
}

.product-category {
    color: #007bff;
    font-size: 0.9em;
    margin: 0 0 8px 0;
    font-weight: 500;
}

.product-price {
    color: #28a745;
    font-size: 1.2em;
    font-weight: bold;
    margin: 0 0 8px 0;
}

.product-description {
    color: #6c757d;
    font-size: 0.9em;
    margin: 0;
    line-height: 1.4;
}

.category-stats {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 15px;
}

.category-item {
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
    border-left: 4px solid #28a745;
}

.category-item h5 {
    margin: 0 0 10px 0;
    color: #495057;
}

.category-item p {
    margin: 5px 0;
    color: #6c757d;
    font-size: 0.9em;
}

@media (max-width: 768px) {
    .filter-controls {
        flex-direction: column;
        align-items: stretch;
    }

    .price-range {
        justify-content: center;
    }

    .product-grid {
        grid-template-columns: 1fr;
    }
}
</style>
