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

<style scoped>
.ref-vs-reactive-demo {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.route-info {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 8px 16px;
  border-radius: 20px;
  font-size: 14px;
  display: inline-block;
  margin-bottom: 30px;
  font-weight: 500;
}

.demo-section {
  margin-bottom: 40px;
  background: #f8f9fa;
  border-radius: 12px;
  padding: 30px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.demo-section h3 {
  color: #2c3e50;
  margin-bottom: 25px;
  font-size: 24px;
  border-bottom: 3px solid #3498db;
  padding-bottom: 10px;
}

/* 對比網格佈局 */
.comparison-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 30px;
  margin-top: 20px;
  align-items: start;
  /* 確保項目從頂部對齊 */
}

.comparison-item {
  background: white;
  border-radius: 12px;
  padding: 25px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  display: flex;
  flex-direction: column;
  height: 100%;
  /* 確保兩個區塊高度一致 */
}

.comparison-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

.ref-item {
  border-left: 5px solid #3498db;
}

.reactive-item {
  border-left: 5px solid #27ae60;
}

.comparison-item h4 {
  color: #2c3e50;
  margin-bottom: 20px;
  font-size: 18px;
  font-weight: 600;
}

/* 控制項樣式 */
.controls {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-bottom: 20px;
  align-items: center;
}

.input-field {
  flex: 1;
  min-width: 120px;
  padding: 10px 15px;
  border: 2px solid #e1e8ed;
  border-radius: 8px;
  font-size: 14px;
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
}

.input-field:focus {
  outline: none;
  border-color: #3498db;
  box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
}

.btn {
  padding: 10px 20px;
  border: none;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  white-space: nowrap;
}

.btn-primary {
  background: linear-gradient(135deg, #3498db, #2980b9);
  color: white;
}

.btn-primary:hover {
  background: linear-gradient(135deg, #2980b9, #1f5f8b);
  transform: translateY(-2px);
}

.btn-success {
  background: linear-gradient(135deg, #27ae60, #229954);
  color: white;
}

.btn-success:hover {
  background: linear-gradient(135deg, #229954, #1e7e34);
  transform: translateY(-2px);
}

/* 結果顯示 */
.result {
  margin-bottom: 20px;
  padding: 15px;
  background: #f8f9fa;
  border-radius: 8px;
  border: 1px solid #e9ecef;
}

.display-value {
  margin-bottom: 8px;
  padding: 8px 12px;
  background: white;
  border-radius: 6px;
  font-family: 'Courier New', monospace;
  font-size: 14px;
  border-left: 4px solid #3498db;
}

.display-value.warning {
  border-left-color: #f39c12;
  background: #fef9e7;
}

.display-value.success {
  border-left-color: #27ae60;
  background: #eafaf1;
}

.note {
  margin: 10px 0;
  padding: 10px;
  background: #fff3cd;
  border: 1px solid #ffeaa7;
  border-radius: 6px;
  color: #856404;
  font-size: 14px;
}

/* 程式碼範例 */
.code-example {
  background: #2c3e50;
  border-radius: 8px;
  overflow: hidden;
  flex: 1;
  /* 讓程式碼區塊填滿剩餘空間 */
  display: flex;
  flex-direction: column;
}

.code-example pre {
  margin: 0;
  padding: 20px;
  color: #ecf0f1;
  font-family: 'Fira Code', 'Courier New', monospace;
  font-size: 13px;
  line-height: 1.6;
  overflow-x: auto;
  flex: 1;
  /* 讓 pre 填滿 code-example 的空間 */
  display: flex;
  align-items: flex-start;
}

.code-example code {
  color: #ecf0f1;
}

/* 建議卡片 */
.recommendation-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 30px;
  margin-top: 20px;
  align-items: start;
  /* 確保卡片從頂部對齊 */
}

.recommendation-card {
  background: white;
  border-radius: 12px;
  padding: 25px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
  display: flex;
  flex-direction: column;
  height: 100%;
  /* 確保兩個卡片高度一致 */
}

.recommendation-card:hover {
  transform: translateY(-3px);
}

.ref-card {
  border-top: 5px solid #3498db;
}

.reactive-card {
  border-top: 5px solid #27ae60;
}

.recommendation-card h4 {
  color: #2c3e50;
  margin-bottom: 20px;
  font-size: 18px;
}

.recommendation-card ul {
  margin-bottom: 20px;
  padding-left: 20px;
  flex: 1;
  /* 讓列表填滿可用空間 */
}

.recommendation-card li {
  margin-bottom: 8px;
  color: #555;
  line-height: 1.5;
}

.example {
  border-top: 1px solid #e9ecef;
  padding-top: 20px;
  flex: 1;
  /* 讓範例區塊填滿剩餘空間 */
  display: flex;
  flex-direction: column;
}

.example h5 {
  color: #2c3e50;
  margin-bottom: 15px;
  font-size: 16px;
}

/* 響應式設計 */
@media (max-width: 768px) {
  .ref-vs-reactive-demo {
    padding: 15px;
  }

  .comparison-grid,
  .recommendation-grid {
    grid-template-columns: 1fr;
    gap: 20px;
  }

  .demo-section {
    padding: 20px;
  }

  .controls {
    flex-direction: column;
    align-items: stretch;
  }

  .input-field {
    min-width: auto;
  }

  .code-example pre {
    font-size: 12px;
    padding: 15px;
  }
}

@media (max-width: 480px) {
  .demo-section h3 {
    font-size: 20px;
  }

  .comparison-item,
  .recommendation-card {
    padding: 20px;
  }

  .route-info {
    font-size: 12px;
    padding: 6px 12px;
  }
}
</style>
