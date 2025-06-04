<!-- components/ReactivitySamples/RefVsReactiveDemo.vue -->
<template>
  <div class="ref-vs-reactive-demo">
    <h2>ref vs reactive 對比</h2>
    <p class="route-info">📍 路徑：/ReactivitySamples/RefVsReactiveDemo.vue</p>

    <!-- 語法對比 -->
    <div class="demo-section">
      <h3>1. 語法對比</h3>
      <div class="comparison-grid">
        <div class="comparison-item ref-item">
          <h4>使用 ref</h4>
          <div class="controls">
            <input v-model="refUser.name" placeholder="姓名" class="input-field">
            <input v-model.number="refUser.age" type="number" placeholder="年齡" class="input-field">
            <button @click="updateRefUser" class="btn btn-primary">更新</button>
          </div>
          <div class="result">
            <div class="display-value">姓名: {{ refUser.name }}</div>
            <div class="display-value">年齡: {{ refUser.age }}</div>
          </div>
          <div class="code-example">
            <pre v-pre><code>// 定義
const refUser = ref({
  name: '',
  age: 0
})

// 修改 (需要 .value)
refUser.value.name = '新名字'
refUser.value = { name: '張三', age: 25 }

// 模板中直接使用
{{ refUser.name }}</code></pre>
          </div>
        </div>

        <div class="comparison-item reactive-item">
          <h4>使用 reactive</h4>
          <div class="controls">
            <input v-model="reactiveUser.name" placeholder="姓名" class="input-field">
            <input v-model.number="reactiveUser.age" type="number" placeholder="年齡" class="input-field">
            <button @click="updateReactiveUser" class="btn btn-success">更新</button>
          </div>
          <div class="result">
            <div class="display-value">姓名: {{ reactiveUser.name }}</div>
            <div class="display-value">年齡: {{ reactiveUser.age }}</div>
          </div>
          <div class="code-example">
            <pre v-pre><code>// 定義
const reactiveUser = reactive({
  name: '',
  age: 0
})

// 修改 (直接使用)
reactiveUser.name = '新名字'
Object.assign(reactiveUser, { name: '李四', age: 30 })

// 模板中直接使用
{{ reactiveUser.name }}</code></pre>
          </div>
        </div>
      </div>
    </div>

    <!-- 解構對比 -->
    <div class="demo-section">
      <h3>2. 解構行為對比</h3>
      <div class="comparison-grid">
        <div class="comparison-item ref-item">
          <h4>ref 解構 (失去響應性)</h4>
          <div class="controls">
            <button @click="changeRefData" class="btn btn-primary">修改原始數據</button>
          </div>
          <div class="result">
            <div class="display-value">原始 refData.count: {{ refData.count }}</div>
            <div class="display-value warning">解構的 refCount: {{ refCount }}</div>
            <p class="note">⚠️ 解構後失去響應性</p>
          </div>
          <div class="code-example">
            <pre v-pre><code>const refData = ref({ count: 0 })

// ❌ 錯誤：失去響應性
const { count } = refData.value

// ✅ 正確：保持響應性
const count = toRef(refData.value, 'count')</code></pre>
          </div>
        </div>

        <div class="comparison-item reactive-item">
          <h4>reactive 解構 (需要 toRefs)</h4>
          <div class="controls">
            <button @click="changeReactiveData" class="btn btn-success">修改原始數據</button>
          </div>
          <div class="result">
            <div class="display-value">原始 reactiveData.count: {{ reactiveData.count }}</div>
            <div class="display-value warning">解構的 reactiveCount: {{ reactiveCount }}</div>
            <div class="display-value success">toRefs 的 refsCount: {{ refsCount }}</div>
          </div>
          <div class="code-example">
            <pre v-pre><code>const reactiveData = reactive({ count: 0 })

// ❌ 錯誤：失去響應性
const { count } = reactiveData

// ✅ 正確：使用 toRefs
const { count } = toRefs(reactiveData)</code></pre>
          </div>
        </div>
      </div>
    </div>

    <!-- 使用建議 -->
    <div class="demo-section">
      <h3>3. 使用建議</h3>
      <div class="recommendation-grid">
        <div class="recommendation-card ref-card">
          <h4>🔧 推薦使用 ref 的情況</h4>
          <ul>
            <li>基本數據類型 (string, number, boolean)</li>
            <li>單一值或簡單物件</li>
            <li>需要重新賦值整個物件</li>
            <li>與第三方庫整合</li>
          </ul>
          <div class="example">
            <h5>範例：</h5>
            <div class="controls">
              <button @click="toggleTheme" class="btn btn-primary">
                切換主題: {{ theme }}
              </button>
            </div>
            <div class="code-example">
              <pre v-pre><code>const theme = ref('light')
const isLoading = ref(false)
const userList = ref([])</code></pre>
            </div>
          </div>
        </div>

        <div class="recommendation-card reactive-card">
          <h4>⚙️ 推薦使用 reactive 的情況</h4>
          <ul>
            <li>複雜的物件結構</li>
            <li>表單數據</li>
            <li>狀態管理</li>
            <li>不需要重新賦值整個物件</li>
          </ul>
          <div class="example">
            <h5>範例：</h5>
            <div class="controls">
              <input v-model="form.username" placeholder="用戶名" class="input-field">
              <input v-model="form.email" placeholder="Email" class="input-field">
            </div>
            <div class="result">
              <div class="display-value">表單: {{ JSON.stringify(form) }}</div>
            </div>
            <div class="code-example">
              <pre v-pre><code>const form = reactive({
  username: '',
  email: '',
  profile: {
    age: 0,
    city: ''
  }
})</code></pre>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, toRefs } from 'vue'

// ref vs reactive 對比
const refUser = ref({
  name: '',
  age: 0
})

const reactiveUser = reactive({
  name: '',
  age: 0
})

// 解構對比
const refData = ref({ count: 0 })
const { count: refCount } = refData.value // 失去響應性

const reactiveData = reactive({ count: 0 })
const { count: reactiveCount } = reactiveData // 失去響應性
const { count: refsCount } = toRefs(reactiveData) // 保持響應性

// 使用建議範例
const theme = ref('light')
const form = reactive({
  username: '',
  email: ''
})

// 方法
const updateRefUser = () => {
  refUser.value = {
    name: '張三 (ref)',
    age: 25
  }
}

const updateReactiveUser = () => {
  Object.assign(reactiveUser, {
    name: '李四 (reactive)',
    age: 30
  })
}

const changeRefData = () => {
  refData.value.count++
}

const changeReactiveData = () => {
  reactiveData.count++
}

const toggleTheme = () => {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
}
</script>
