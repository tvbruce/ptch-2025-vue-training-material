<template>
  <div class="shopping-cart-practice">
    <h2>🛒 購物車練習 - v-for 列表渲染</h2>
    <p class="route-info">📍 路徑：/ListSamples/ShoppingCartPractice.vue</p>
    <p class="description">
      📝 <strong>練習目標：</strong>學習使用 v-for 渲染商品列表、動態添加刪除項目、計算總價
    </p>

    <div class="demo-section">
      <h3>🎯 練習任務</h3>
      <div class="task-list">
        <div class="task-item">
          <span>✅ 1. 使用 v-for 渲染商品列表</span>
        </div>
        <div class="task-item">
          <span>✅ 2. 實現添加商品到購物車功能</span>
        </div>
        <div class="task-item">
          <span>✅ 3. 實現刪除購物車商品功能</span>
        </div>
        <div class="task-item">
          <span>✅ 4. 動態計算購物車總價</span>
        </div>
      </div>
    </div>

    <div class="demo-section">
      <h3>🏪 商品列表</h3>
      <div class="product-grid">
        <div v-for="product in products" :key="product.id" class="product-card">
          <div class="product-image">{{ product.emoji }}</div>
          <div class="product-info">
            <h4>{{ product.name }}</h4>
            <p class="product-price">${{ product.price }}</p>
            <button @click="addToCart(product)" class="btn btn-primary btn-sm">
              加入購物車
            </button>
          </div>
        </div>
      </div>
    </div>

    <div class="demo-section">
      <h3>🛒 購物車 ({{ cartItems.length }} 件商品)</h3>
      <div v-if="cartItems.length === 0" class="empty-cart">
        購物車是空的，快去選購商品吧！
      </div>
      <div v-else>
        <div v-for="item in cartItems" :key="item.id" class="cart-item">
          <span class="item-emoji">{{ item.emoji }}</span>
          <div class="item-details">
            <span class="item-name">{{ item.name }}</span>
            <span class="item-price">${{ item.price }}</span>
          </div>
          <div class="item-quantity">
            <button @click="decreaseQuantity(item.id)" class="btn btn-sm btn-secondary">
              -
            </button>
            <span class="quantity">{{ item.quantity }}</span>
            <button @click="increaseQuantity(item.id)" class="btn btn-sm btn-secondary">
              +
            </button>
          </div>
          <div class="item-total">${{ (item.price * item.quantity).toFixed(2) }}</div>
          <button @click="removeFromCart(item.id)" class="btn btn-danger btn-sm">
            刪除
          </button>
        </div>

        <div class="cart-summary">
          <div class="total-price">
            總計：${{ cartTotal.toFixed(2) }}
          </div>
          <button @click="clearCart" class="btn btn-warning">
            清空購物車
          </button>
        </div>
      </div>
    </div>

    <div class="code-example">
      <h4>💻 關鍵代碼</h4>
      <pre v-pre><code>// 商品列表渲染
&lt;div v-for="product in products" :key="product.id"&gt;
  {{ product.name }} - ${{ product.price }}
&lt;/div&gt;

// 購物車渲染
&lt;div v-for="item in cartItems" :key="item.id"&gt;
  {{ item.name }} x {{ item.quantity }}
&lt;/div&gt;

// 響應式數據
const products = ref([...])
const cartItems = ref([])

// 計算總價
const cartTotal = computed(() =&gt; {
  return cartItems.value.reduce((total, item) =&gt; {
    return total + (item.price * item.quantity)
  }, 0)
})</code></pre>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 商品數據
const products = ref([
  { id: 1, name: '蘋果', price: 2.5, emoji: '🍎' },
  { id: 2, name: '香蕉', price: 1.8, emoji: '🍌' },
  { id: 3, name: '橘子', price: 3.0, emoji: '🍊' },
  { id: 4, name: '葡萄', price: 4.2, emoji: '🍇' },
  { id: 5, name: '草莓', price: 3.8, emoji: '🍓' },
  { id: 6, name: '西瓜', price: 5.0, emoji: '🍉' },
  { id: 7, name: '鳳梨', price: 4.5, emoji: '🍍' },
  { id: 8, name: '桃子', price: 3.2, emoji: '🍑' }
])

// 購物車數據
const cartItems = ref([])

// 計算購物車總價
const cartTotal = computed(() => {
  return cartItems.value.reduce((total, item) => {
    return total + (item.price * item.quantity)
  }, 0)
})

// 添加商品到購物車
const addToCart = (product) => {
  const existingItem = cartItems.value.find(item => item.id === product.id)

  if (existingItem) {
    existingItem.quantity++
  } else {
    cartItems.value.push({
      ...product,
      quantity: 1
    })
  }
}

// 移除商品
const removeFromCart = (productId) => {
  const index = cartItems.value.findIndex(item => item.id === productId)
  if (index > -1) {
    cartItems.value.splice(index, 1)
  }
}

// 增加數量
const increaseQuantity = (productId) => {
  const item = cartItems.value.find(item => item.id === productId)
  if (item) {
    item.quantity++
  }
}

// 減少數量
const decreaseQuantity = (productId) => {
  const item = cartItems.value.find(item => item.id === productId)
  if (item && item.quantity > 1) {
    item.quantity--
  } else if (item && item.quantity === 1) {
    removeFromCart(productId)
  }
}

// 清空購物車
const clearCart = () => {
  cartItems.value = []
}
</script>

<style scoped>
.product-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 1rem;
  margin: 1rem 0;
}

.product-card {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 1rem;
  text-align: center;
  background: white;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.product-image {
  font-size: 3rem;
  margin-bottom: 0.5rem;
}

.product-price {
  font-weight: bold;
  color: #e74c3c;
  font-size: 1.2rem;
}

.cart-item {
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 1rem;
  border: 1px solid #ddd;
  border-radius: 8px;
  margin-bottom: 0.5rem;
  background: white;
}

.item-emoji {
  font-size: 2rem;
}

.item-details {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.item-name {
  font-weight: bold;
}

.item-quantity {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.quantity {
  min-width: 2rem;
  text-align: center;
  font-weight: bold;
}

.item-total {
  font-weight: bold;
  color: #e74c3c;
  min-width: 80px;
}

.cart-summary {
  border-top: 2px solid #ddd;
  padding-top: 1rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 1rem;
}

.total-price {
  font-size: 1.5rem;
  font-weight: bold;
  color: #27ae60;
}

.empty-cart {
  text-align: center;
  padding: 2rem;
  color: #666;
  font-style: italic;
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
</style>
