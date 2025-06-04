<!-- components/ReactivitySamples/RefBasicsDemo.vue -->
<template>
  <div class="ref-basics-demo">
    <h2>ref 基礎用法</h2>
    <p class="route-info">📍 路徑：/ReactivitySamples/RefBasicsDemo.vue</p>

    <!-- 基本數值 -->
    <div class="demo-section">
      <h3>1. 基本數值類型</h3>
      <div class="controls">
        <button @click="count++" class="btn btn-primary">增加</button>
        <button @click="count--" class="btn btn-secondary">減少</button>
        <button @click="count = 0" class="btn btn-danger">重置</button>
      </div>
      <div class="result">
        <div class="display-value">計數器: {{ count }}</div>
      </div>
      <div class="code-example">
        <pre v-pre><code>const count = ref(0)

// 在模板中直接使用
{{ count }}

// 在 script 中需要 .value
count.value++</code></pre>
      </div>
    </div>

    <!-- 字串 -->
    <div class="demo-section">
      <h3>2. 字串類型</h3>
      <div class="controls">
        <input v-model="message" placeholder="輸入訊息..." class="input-field">
        <button @click="clearMessage" class="btn btn-secondary">清空</button>
      </div>
      <div class="result">
        <div class="display-value">訊息: {{ message || '(空白)' }}</div>
        <div class="display-value">長度: {{ message.length }}</div>
      </div>
      <div class="code-example">
        <pre v-pre><code>const message = ref('')

// 雙向綁定
&lt;input v-model="message"&gt;

// 顯示內容
{{ message }}</code></pre>
      </div>
    </div>

    <!-- 布林值 -->
    <div class="demo-section">
      <h3>3. 布林值類型</h3>
      <div class="controls">
        <label class="checkbox-label">
          <input type="checkbox" v-model="isVisible">
          顯示內容
        </label>
        <button @click="toggleVisibility" class="btn btn-primary">切換</button>
      </div>
      <div class="result">
        <div v-if="isVisible" class="display-value success">
          ✅ 內容已顯示 (isVisible: {{ isVisible }})
        </div>
        <div v-else class="display-value info">
          ❌ 內容已隱藏 (isVisible: {{ isVisible }})
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>const isVisible = ref(true)

// 條件渲染
&lt;div v-if="isVisible"&gt;內容&lt;/div&gt;

// 切換方法
const toggleVisibility = () => {
  isVisible.value = !isVisible.value
}</code></pre>
      </div>
    </div>

    <!-- 物件 -->
    <div class="demo-section">
      <h3>4. 物件類型</h3>
      <div class="controls">
        <input v-model="user.name" placeholder="姓名" class="input-field">
        <input v-model.number="user.age" type="number" placeholder="年齡" class="input-field">
        <button @click="resetUser" class="btn btn-secondary">重置</button>
      </div>
      <div class="result">
        <div class="display-value">姓名: {{ user.name || '(未設定)' }}</div>
        <div class="display-value">年齡: {{ user.age || '(未設定)' }}</div>
        <div class="display-value">完整物件: {{ JSON.stringify(user) }}</div>
      </div>
      <div class="code-example">
        <pre v-pre><code>const user = ref({
  name: '',
  age: 0
})

// 修改屬性
user.value.name = '新名字'
user.value.age = 25

// 在模板中直接使用
{{ user.name }}</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// 基本數值
const count = ref(0)

// 字串
const message = ref('')

// 布林值
const isVisible = ref(true)

// 物件
const user = ref({
  name: '',
  age: 0
})

// 方法
const clearMessage = () => {
  message.value = ''
}

const toggleVisibility = () => {
  isVisible.value = !isVisible.value
}

const resetUser = () => {
  user.value = {
    name: '',
    age: 0
  }
}
</script>
