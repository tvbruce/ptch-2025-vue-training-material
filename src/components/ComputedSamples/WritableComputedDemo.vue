<!-- components/ComputedSamples/WritableComputedDemo.vue -->
<template>
  <div class="writable-computed-demo">
    <h2>可寫計算屬性 (Writable Computed)</h2>
    <p class="route-info">📍 路徑：/ComputedSamples/WritableComputedDemo.vue</p>

    <!-- 姓名拆分合併 -->
    <div class="demo-section">
      <h3>1. 姓名拆分與合併</h3>
      <div class="controls">
        <input v-model="firstName" placeholder="名字" class="input-field">
        <input v-model="lastName" placeholder="姓氏" class="input-field">
      </div>
      <div class="result">
        <div class="display-item">
          <label>完整姓名 (可直接編輯)：</label>
          <input v-model="fullName" class="computed-input" placeholder="直接輸入完整姓名">
        </div>
        <div class="info-box">
          <p><strong>說明：</strong>當你在上方輸入框中輸入完整姓名時，會自動拆分為名字和姓氏</p>
          <p>例如：輸入 "王小明" 會自動設定名字為 "小明"，姓氏為 "王"</p>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 可寫計算屬性 - 姓名範例
const firstName = ref('')
const lastName = ref('')

const fullName = computed({
  // getter: 當讀取時執行
  get() {
    return firstName.value + lastName.value
  },
  // setter: 當寫入時執行
  set(newValue) {
    if (newValue.length >= 2) {
      lastName.value = newValue.charAt(0)      // 第一個字為姓
      firstName.value = newValue.slice(1)      // 其餘為名
    }
  }
})</code></pre>
      </div>
    </div>

    <!-- 溫度轉換 -->
    <div class="demo-section">
      <h3>2. 溫度單位轉換</h3>
      <div class="controls">
        <div class="temperature-inputs">
          <div class="temp-input-group">
            <label>攝氏溫度 (°C)：</label>
            <input v-model.number="celsius" type="number" class="input-field">
          </div>
          <div class="temp-input-group">
            <label>華氏溫度 (°F)：</label>
            <input v-model.number="fahrenheit" type="number" class="input-field">
          </div>
        </div>
      </div>
      <div class="result">
        <div class="temperature-display">
          <div class="temp-card">
            <h4>攝氏</h4>
            <div class="temp-value">{{ celsius }}°C</div>
          </div>
          <div class="conversion-arrow">⇄</div>
          <div class="temp-card">
            <h4>華氏</h4>
            <div class="temp-value">{{ fahrenheit }}°F</div>
          </div>
        </div>
        <div class="info-box">
          <p><strong>說明：</strong>修改任一溫度值，另一個會自動轉換</p>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 可寫計算屬性 - 溫度轉換
const celsius = ref(0)

const fahrenheit = computed({
  get() {
    return (celsius.value * 9/5 + 32).toFixed(1)
  },
  set(newValue) {
    celsius.value = ((newValue - 32) * 5/9).toFixed(1)
  }
})</code></pre>
      </div>
    </div>

    <!-- 購物車總價 -->
    <div class="demo-section">
      <h3>3. 購物車價格計算</h3>
      <div class="controls">
        <div class="cart-controls">
          <button @click="addItem" class="btn btn-primary">
            添加商品
          </button>
          <button @click="clearCart" class="btn btn-secondary">
            清空購物車
          </button>
        </div>
      </div>
      <div class="result">
        <div class="cart-items">
          <div v-for="(item, index) in cartItems" :key="index" class="cart-item">
            <span class="item-name">{{ item.name }}</span>
            <input v-model.number="item.quantity" type="number" min="1" class="quantity-input">
            <span class="item-price">${{ item.price }}</span>
            <button @click="removeItem(index)" class="btn-remove">×</button>
          </div>
          <div v-if="cartItems.length === 0" class="empty-cart">
            購物車是空的
          </div>
        </div>

        <div class="cart-summary">
          <div class="summary-row">
            <span>商品總數：</span>
            <span>{{ totalItems }} 件</span>
          </div>
          <div class="summary-row">
            <span>小計：</span>
            <span>${{ subtotalAmount }}</span>
          </div>
          <div class="summary-row">
            <label>折扣 (%)：</label>
            <input v-model.number="discountPercent" type="number" min="0" max="100" class="discount-input">
          </div>
          <div class="summary-row total">
            <span>總計：</span>
            <input v-model.number="totalAmount" class="total-input" placeholder="可直接修改總金額">
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 可寫計算屬性 - 購物車總價
const cartItems = ref([])
const discountPercent = ref(0)

const subtotalAmount = computed(() => {
  return cartItems.value.reduce((sum, item) =>
    sum + (item.price * item.quantity), 0
  ).toFixed(2)
})

const totalAmount = computed({
  get() {
    const discount = subtotalAmount.value * (discountPercent.value / 100)
    return (subtotalAmount.value - discount).toFixed(2)
  },
  set(newValue) {
    // 反推折扣比例
    const newDiscount = subtotalAmount.value - newValue
    discountPercent.value = ((newDiscount / subtotalAmount.value) * 100).toFixed(1)
  }
})</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 姓名拆分合併
const firstName = ref('')
const lastName = ref('')

const fullName = computed({
  get() {
    return firstName.value + lastName.value
  },
  set(newValue) {
    if (newValue.length >= 2) {
      lastName.value = newValue.charAt(0)
      firstName.value = newValue.slice(1)
    } else if (newValue.length === 1) {
      lastName.value = newValue
      firstName.value = ''
    } else {
      lastName.value = ''
      firstName.value = ''
    }
  }
})

// 溫度轉換
const celsius = ref(0)

const fahrenheit = computed({
  get() {
    return (celsius.value * 9 / 5 + 32).toFixed(1)
  },
  set(newValue) {
    celsius.value = ((newValue - 32) * 5 / 9).toFixed(1)
  }
})

// 購物車
const cartItems = ref([
  { name: '蘋果', price: 1.5, quantity: 2 },
  { name: '香蕉', price: 0.8, quantity: 3 }
])
const discountPercent = ref(0)

const totalItems = computed(() => {
  return cartItems.value.reduce((sum, item) => sum + item.quantity, 0)
})

const subtotalAmount = computed(() => {
  return cartItems.value.reduce((sum, item) =>
    sum + (item.price * item.quantity), 0
  ).toFixed(2)
})

const totalAmount = computed({
  get() {
    const discount = subtotalAmount.value * (discountPercent.value / 100)
    return (subtotalAmount.value - discount).toFixed(2)
  },
  set(newValue) {
    if (subtotalAmount.value > 0) {
      const newDiscount = subtotalAmount.value - newValue
      discountPercent.value = Math.max(0, Math.min(100,
        ((newDiscount / subtotalAmount.value) * 100)
      )).toFixed(1)
    }
  }
})

// 方法
const addItem = () => {
  const items = ['橘子', '葡萄', '草莓', '西瓜', '芒果']
  const randomItem = items[Math.floor(Math.random() * items.length)]
  const randomPrice = (Math.random() * 3 + 0.5).toFixed(1)

  cartItems.value.push({
    name: randomItem,
    price: parseFloat(randomPrice),
    quantity: 1
  })
}

const removeItem = (index) => {
  cartItems.value.splice(index, 1)
}

const clearCart = () => {
  cartItems.value = []
  discountPercent.value = 0
}
</script>

<style scoped>
/* 組件樣式已在全域 main.css 中定義 */
</style>
