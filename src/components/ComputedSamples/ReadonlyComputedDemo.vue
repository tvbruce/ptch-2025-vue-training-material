<!-- components/ComputedSamples/ReadonlyComputedDemo.vue -->
<template>
  <div class="readonly-computed-demo">
    <h2>唯讀計算屬性 (Readonly Computed)</h2>
    <p class="route-info">📍 路徑：/ComputedSamples/ReadonlyComputedDemo.vue</p>

    <!-- 基本計算屬性 -->
    <div class="demo-section">
      <h3>1. 基本計算屬性</h3>
      <div class="controls">
        <input v-model="firstName" placeholder="名字" class="input-field">
        <input v-model="lastName" placeholder="姓氏" class="input-field">
      </div>
      <div class="result">
        <div class="display-item">
          <label>完整姓名：</label>
          <span class="computed-value">{{ fullName }}</span>
        </div>
        <div class="display-item">
          <label>姓名長度：</label>
          <span class="computed-value">{{ nameLength }} 個字符</span>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 基本計算屬性
const firstName = ref('')
const lastName = ref('')

// 計算屬性會自動追蹤依賴並快取結果
const fullName = computed(() => {
  return firstName.value + ' ' + lastName.value
})

const nameLength = computed(() => {
  return fullName.value.trim().length
})</code></pre>
      </div>
    </div>

    <!-- 數字計算 -->
    <div class="demo-section">
      <h3>2. 數字計算範例</h3>
      <div class="controls">
        <input v-model.number="price" type="number" placeholder="商品價格" class="input-field">
        <input v-model.number="quantity" type="number" placeholder="數量" class="input-field">
        <input v-model.number="taxRate" type="number" step="0.01" placeholder="稅率 (0.1 = 10%)" class="input-field">
      </div>
      <div class="result">
        <div class="calculation-display">
          <div class="calc-row">
            <span>小計：</span>
            <span class="computed-value">${{ subtotal }}</span>
          </div>
          <div class="calc-row">
            <span>稅額：</span>
            <span class="computed-value">${{ taxAmount }}</span>
          </div>
          <div class="calc-row total">
            <span>總計：</span>
            <span class="computed-value">${{ total }}</span>
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 數字計算
const price = ref(0)
const quantity = ref(0)
const taxRate = ref(0.1)

const subtotal = computed(() => {
  return (price.value * quantity.value).toFixed(2)
})

const taxAmount = computed(() => {
  return (subtotal.value * taxRate.value).toFixed(2)
})

const total = computed(() => {
  return (parseFloat(subtotal.value) + parseFloat(taxAmount.value)).toFixed(2)
})</code></pre>
      </div>
    </div>

    <!-- 陣列過濾 -->
    <div class="demo-section">
      <h3>3. 陣列過濾計算</h3>
      <div class="controls">
        <input v-model="searchTerm" placeholder="搜尋水果名稱" class="input-field">
        <select v-model="priceFilter" class="select-field">
          <option value="all">所有價格</option>
          <option value="cheap">便宜 (< $2)</option>
          <option value="expensive">昂貴 (>= $2)</option>
        </select>
      </div>
      <div class="result">
        <div class="fruit-list">
          <div v-for="fruit in filteredFruits" :key="fruit.id" class="fruit-item">
            <span class="fruit-name">{{ fruit.name }}</span>
            <span class="fruit-price">${{ fruit.price }}</span>
          </div>
          <div v-if="filteredFruits.length === 0" class="no-results">
            沒有找到符合條件的水果
          </div>
        </div>
        <div class="summary">
          <span>顯示 {{ filteredFruits.length }} / {{ fruits.length }} 項商品</span>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 陣列過濾計算
const searchTerm = ref('')
const priceFilter = ref('all')
const fruits = ref([
  { id: 1, name: '蘋果', price: 1.5 },
  { id: 2, name: '香蕉', price: 0.8 },
  { id: 3, name: '橘子', price: 2.2 },
  { id: 4, name: '葡萄', price: 3.0 }
])

const filteredFruits = computed(() => {
  let result = fruits.value

  // 按名稱搜尋
  if (searchTerm.value) {
    result = result.filter(fruit =>
      fruit.name.includes(searchTerm.value)
    )
  }

  // 按價格過濾
  if (priceFilter.value === 'cheap') {
    result = result.filter(fruit => fruit.price < 2)
  } else if (priceFilter.value === 'expensive') {
    result = result.filter(fruit => fruit.price >= 2)
  }

  return result
})</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 基本計算屬性
const firstName = ref('')
const lastName = ref('')

const fullName = computed(() => {
  return firstName.value + ' ' + lastName.value
})

const nameLength = computed(() => {
  return fullName.value.trim().length
})

// 數字計算
const price = ref(0)
const quantity = ref(0)
const taxRate = ref(0.1)

const subtotal = computed(() => {
  return (price.value * quantity.value).toFixed(2)
})

const taxAmount = computed(() => {
  return (subtotal.value * taxRate.value).toFixed(2)
})

const total = computed(() => {
  return (parseFloat(subtotal.value) + parseFloat(taxAmount.value)).toFixed(2)
})

// 陣列過濾
const searchTerm = ref('')
const priceFilter = ref('all')
const fruits = ref([
  { id: 1, name: '蘋果', price: 1.5 },
  { id: 2, name: '香蕉', price: 0.8 },
  { id: 3, name: '橘子', price: 2.2 },
  { id: 4, name: '葡萄', price: 3.0 },
  { id: 5, name: '草莓', price: 2.8 },
  { id: 6, name: '西瓜', price: 1.2 }
])

const filteredFruits = computed(() => {
  let result = fruits.value

  // 按名稱搜尋
  if (searchTerm.value) {
    result = result.filter(fruit =>
      fruit.name.includes(searchTerm.value)
    )
  }

  // 按價格過濾
  if (priceFilter.value === 'cheap') {
    result = result.filter(fruit => fruit.price < 2)
  } else if (priceFilter.value === 'expensive') {
    result = result.filter(fruit => fruit.price >= 2)
  }

  return result
})
</script>

<style scoped>
/* 組件樣式已在全域 main.css 中定義 */
</style>
