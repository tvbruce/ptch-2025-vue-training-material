<!-- components/ReactivitySamples/ReactiveBasicsDemo.vue -->
<template>
  <div class="reactive-basics-demo">
    <h2>reactive 基礎用法</h2>
    <p class="route-info">📍 路徑：/ReactivitySamples/ReactiveBasicsDemo.vue</p>

    <!-- 基本物件 -->
    <div class="demo-section">
      <h3>1. 基本物件響應</h3>
      <div class="controls">
        <input v-model="person.name" placeholder="姓名" class="input-field">
        <input v-model.number="person.age" type="number" placeholder="年齡" class="input-field">
        <button @click="resetPerson" class="btn btn-secondary">重置</button>
      </div>
      <div class="result">
        <div class="display-value">姓名: {{ person.name || '(未設定)' }}</div>
        <div class="display-value">年齡: {{ person.age || '(未設定)' }}</div>
        <div class="display-value">完整物件: {{ JSON.stringify(person) }}</div>
      </div>
      <div class="code-example">
        <pre v-pre><code>const person = reactive({
  name: '',
  age: 0
})

// 直接修改屬性，無需 .value
person.name = '張三'
person.age = 25

// 在模板中直接使用
{{ person.name }}</code></pre>
      </div>
    </div>

    <!-- 陣列操作 -->
    <div class="demo-section">
      <h3>2. 陣列響應</h3>
      <div class="controls">
        <input v-model="newItem" placeholder="新項目" class="input-field" @keyup.enter="addItem">
        <button @click="addItem" class="btn btn-primary">新增</button>
        <button @click="clearItems" class="btn btn-danger">清空</button>
      </div>
      <div class="result">
        <div class="display-value">項目數量: {{ items.length }}</div>
        <div class="item-list">
          <div v-for="(item, index) in items" :key="index" class="item">
            <span>{{ item }}</span>
            <button @click="removeItem(index)" class="btn-small">刪除</button>
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>const items = reactive([])

// 陣列操作
items.push('新項目')
items.splice(index, 1)

// 在模板中遍歷
&lt;div v-for="item in items"&gt;{{ item }}&lt;/div&gt;</code></pre>
      </div>
    </div>

    <!-- 巢狀物件 -->
    <div class="demo-section">
      <h3>3. 巢狀物件響應</h3>
      <div class="controls">
        <input v-model="profile.personal.name" placeholder="姓名" class="input-field">
        <input v-model="profile.personal.email" placeholder="Email" class="input-field">
        <input v-model="profile.settings.theme" placeholder="主題" class="input-field">
        <label class="checkbox-label">
          <input type="checkbox" v-model="profile.settings.notifications">
          接收通知
        </label>
      </div>
      <div class="result">
        <div class="display-value">個人資料: {{ JSON.stringify(profile.personal) }}</div>
        <div class="display-value">設定: {{ JSON.stringify(profile.settings) }}</div>
      </div>
      <div class="code-example">
        <pre v-pre><code>const profile = reactive({
  personal: {
    name: '',
    email: ''
  },
  settings: {
    theme: 'light',
    notifications: true
  }
})

// 深層屬性也是響應式的
profile.personal.name = '李四'
profile.settings.theme = 'dark'</code></pre>
      </div>
    </div>

    <!-- 計算屬性配合 -->
    <div class="demo-section">
      <h3>4. 配合計算屬性</h3>
      <div class="controls">
        <input v-model="cart.items[0].name" placeholder="商品1名稱" class="input-field">
        <input v-model.number="cart.items[0].price" type="number" placeholder="價格" class="input-field">
        <input v-model.number="cart.items[0].quantity" type="number" placeholder="數量" class="input-field">
      </div>
      <div class="result">
        <div class="display-value">商品: {{ cart.items[0].name || '(未設定)' }}</div>
        <div class="display-value">單價: ${{ cart.items[0].price || 0 }}</div>
        <div class="display-value">數量: {{ cart.items[0].quantity || 0 }}</div>
        <div class="display-value total">總金額: ${{ totalPrice }}</div>
      </div>
      <div class="code-example">
        <pre v-pre><code>const cart = reactive({
  items: [
    { name: '', price: 0, quantity: 0 }
  ]
})

// 計算屬性會自動響應變化
const totalPrice = computed(() => {
  return cart.items.reduce((sum, item) => {
    return sum + (item.price * item.quantity)
  }, 0)
})</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref, computed } from 'vue'

// 基本物件
const person = reactive({
  name: '',
  age: 0
})

// 陣列
const items = reactive([])
const newItem = ref('')

// 巢狀物件
const profile = reactive({
  personal: {
    name: '',
    email: ''
  },
  settings: {
    theme: 'light',
    notifications: true
  }
})

// 購物車
const cart = reactive({
  items: [
    { name: '', price: 0, quantity: 0 }
  ]
})

// 計算屬性
const totalPrice = computed(() => {
  return cart.items.reduce((sum, item) => {
    return sum + (item.price * item.quantity)
  }, 0)
})

// 方法
const resetPerson = () => {
  person.name = ''
  person.age = 0
}

const addItem = () => {
  if (newItem.value.trim()) {
    items.push(newItem.value.trim())
    newItem.value = ''
  }
}

const removeItem = (index) => {
  items.splice(index, 1)
}

const clearItems = () => {
  items.splice(0, items.length)
}
</script>
