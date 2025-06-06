<!-- components/ReactivitySamples/WithoutReactivityDemo.vue -->
<template>
  <div class="without-reactivity-demo">
    <h2>沒有響應式的對比</h2>
    <p class="route-info">📍 路徑：/ReactivitySamples/WithoutReactivityDemo.vue</p>

    <!-- 普通變數 vs 響應式變數 -->
    <div class="demo-section">
      <h3>1. 普通變數 vs 響應式變數</h3>
      <div class="comparison-grid">
        <div class="comparison-item normal-item">
          <h4>❌ 普通變數 (不響應)</h4>
          <div class="controls">
            <button @click="incrementNormal" class="btn btn-danger">
              增加普通計數
            </button>
            <button @click="forceUpdate" class="btn btn-warning">
              強制更新畫面
            </button>
          </div>
          <div class="result">
            <div class="display-value warning">
              普通計數: {{ normalCount }}
            </div>
            <div class="display-value">
              實際值: {{ getNormalCount() }}
            </div>
            <p class="note">⚠️ 畫面不會自動更新</p>
          </div>
          <div class="code-example">
            <pre v-pre><code>// ❌ 普通變數
let normalCount = 0

const incrementNormal = () => {
  normalCount++ // 畫面不會更新
}

// 需要手動觸發更新
const forceUpdate = () => {
  // 使用 $forceUpdate 或其他方式
}</code></pre>
          </div>
        </div>

        <div class="comparison-item reactive-item">
          <h4>✅ 響應式變數 (自動響應)</h4>
          <div class="controls">
            <button @click="incrementReactive" class="btn btn-success">
              增加響應式計數
            </button>
          </div>
          <div class="result">
            <div class="display-value success">
              響應式計數: {{ reactiveCount }}
            </div>
            <p class="note">✅ 畫面自動更新</p>
          </div>
          <div class="code-example">
            <pre v-pre><code>// ✅ 響應式變數
const reactiveCount = ref(0)

const incrementReactive = () => {
  reactiveCount.value++ // 畫面自動更新
}</code></pre>
          </div>
        </div>
      </div>
    </div>

    <!-- 物件屬性對比 -->
    <div class="demo-section">
      <h3>2. 物件屬性對比</h3>
      <div class="comparison-grid">
        <div class="comparison-item normal-item">
          <h4>❌ 普通物件 (不響應)</h4>
          <div class="controls">
            <input :value="normalUser.name" @input="updateNormalUserName" placeholder="姓名" class="input-field">
            <input :value="normalUser.age" @input="updateNormalUserAge" type="number" placeholder="年齡"
              class="input-field">
          </div>
          <div class="result">
            <div class="display-value warning">
              顯示姓名: {{ normalUser.name }}
            </div>
            <div class="display-value warning">
              顯示年齡: {{ normalUser.age }}
            </div>
            <div class="display-value">
              實際物件: {{ JSON.stringify(getNormalUser()) }}
            </div>
            <p class="note">⚠️ 需要手動綁定事件</p>
          </div>
          <div class="code-example">
            <pre v-pre><code>// ❌ 普通物件
let normalUser = { name: '', age: 0 }

// 需要手動處理輸入
const updateNormalUserName = (e) => {
  normalUser.name = e.target.value
  // 畫面不會自動更新
}</code></pre>
          </div>
        </div>

        <div class="comparison-item reactive-item">
          <h4>✅ 響應式物件 (自動響應)</h4>
          <div class="controls">
            <input v-model="reactiveUser.name" placeholder="姓名" class="input-field">
            <input v-model.number="reactiveUser.age" type="number" placeholder="年齡" class="input-field">
          </div>
          <div class="result">
            <div class="display-value success">
              顯示姓名: {{ reactiveUser.name }}
            </div>
            <div class="display-value success">
              顯示年齡: {{ reactiveUser.age }}
            </div>
            <p class="note">✅ v-model 自動雙向綁定</p>
          </div>
          <div class="code-example">
            <pre v-pre><code>// ✅ 響應式物件
const reactiveUser = reactive({ name: '', age: 0 })

// 自動雙向綁定
&lt;input v-model="reactiveUser.name"&gt;</code></pre>
          </div>
        </div>
      </div>
    </div>

    <!-- 列表操作對比 -->
    <div class="demo-section">
      <h3>3. 列表操作對比</h3>
      <div class="comparison-grid">
        <div class="comparison-item normal-item">
          <h4>❌ 普通陣列 (不響應)</h4>
          <div class="controls">
            <input v-model="newNormalItem" placeholder="新項目" class="input-field" @keyup.enter="addNormalItem">
            <button @click="addNormalItem" class="btn btn-danger">
              新增到普通陣列
            </button>
            <button @click="forceUpdateList" class="btn btn-warning">
              強制更新列表
            </button>
          </div>
          <div class="result">
            <div class="display-value warning">
              顯示項目數: {{ normalItems.length }}
            </div>
            <div class="display-value">
              實際項目數: {{ getNormalItems().length }}
            </div>
            <div class="item-list">
              <div v-for="(item, index) in normalItems" :key="`normal-${index}`" class="item warning">
                {{ item }}
              </div>
            </div>
            <p class="note">⚠️ 列表不會自動更新</p>
          </div>
          <div class="code-example">
            <pre v-pre><code>// ❌ 普通陣列
let normalItems = []

const addNormalItem = () => {
  normalItems.push(newItem)
  // 畫面不會更新
}</code></pre>
          </div>
        </div>

        <div class="comparison-item reactive-item">
          <h4>✅ 響應式陣列 (自動響應)</h4>
          <div class="controls">
            <input v-model="newReactiveItem" placeholder="新項目" class="input-field" @keyup.enter="addReactiveItem">
            <button @click="addReactiveItem" class="btn btn-success">
              新增到響應式陣列
            </button>
          </div>
          <div class="result">
            <div class="display-value success">
              顯示項目數: {{ reactiveItems.length }}
            </div>
            <div class="item-list">
              <div v-for="(item, index) in reactiveItems" :key="`reactive-${index}`" class="item success">
                <span>{{ item }}</span>
                <button @click="removeReactiveItem(index)" class="btn-small">
                  刪除
                </button>
              </div>
            </div>
            <p class="note">✅ 列表自動更新</p>
          </div>
          <div class="code-example">
            <pre v-pre><code>// ✅ 響應式陣列
const reactiveItems = reactive([])

const addReactiveItem = () => {
  reactiveItems.push(newItem)
  // 畫面自動更新
}</code></pre>
          </div>
        </div>
      </div>
    </div>

    <!-- 總結 -->
    <div class="demo-section">
      <h3>4. 總結對比</h3>
      <div class="summary-table">
        <div class="table-header">
          <span>特性</span>
          <span>普通變數/物件</span>
          <span>響應式 (ref/reactive)</span>
        </div>
        <div class="table-row">
          <span>畫面更新</span>
          <span class="normal-cell">❌ 需要手動觸發</span>
          <span class="reactive-cell">✅ 自動更新</span>
        </div>
        <div class="table-row">
          <span>雙向綁定</span>
          <span class="normal-cell">❌ 需要手動處理</span>
          <span class="reactive-cell">✅ v-model 自動綁定</span>
        </div>
        <div class="table-row">
          <span>計算屬性</span>
          <span class="normal-cell">❌ 無法依賴追蹤</span>
          <span class="reactive-cell">✅ 自動依賴追蹤</span>
        </div>
        <div class="table-row">
          <span>監聽器</span>
          <span class="normal-cell">❌ 無法監聽變化</span>
          <span class="reactive-cell">✅ watch/watchEffect</span>
        </div>
        <div class="table-row">
          <span>開發體驗</span>
          <span class="normal-cell">❌ 需要更多手動代碼</span>
          <span class="reactive-cell">✅ 簡潔直觀</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, nextTick } from 'vue'

// 普通變數 (不響應)
let normalCount = 0
let normalUser = { name: '', age: 0 }
let normalItems = []

// 響應式變數
const reactiveCount = ref(0)
const reactiveUser = reactive({ name: '', age: 0 })
const reactiveItems = reactive([])

// 輸入框
const newNormalItem = ref('')
const newReactiveItem = ref('')

// 強制更新標記
const forceUpdateFlag = ref(0)

// 普通變數操作
const incrementNormal = () => {
  normalCount++
  console.log('普通計數已增加到:', normalCount)
}

const updateNormalUserName = (e) => {
  normalUser.name = e.target.value
  console.log('普通用戶姓名已更新為:', normalUser.name)
}

const updateNormalUserAge = (e) => {
  normalUser.age = parseInt(e.target.value) || 0
  console.log('普通用戶年齡已更新為:', normalUser.age)
}

const addNormalItem = () => {
  if (newNormalItem.value.trim()) {
    normalItems.push(newNormalItem.value.trim())
    newNormalItem.value = ''
    console.log('普通陣列已新增項目，當前長度:', normalItems.length)
  }
}

// 響應式變數操作
const incrementReactive = () => {
  reactiveCount.value++
}

const addReactiveItem = () => {
  if (newReactiveItem.value.trim()) {
    reactiveItems.push(newReactiveItem.value.trim())
    newReactiveItem.value = ''
  }
}

const removeReactiveItem = (index) => {
  reactiveItems.splice(index, 1)
}

// 強制更新方法
const forceUpdate = () => {
  forceUpdateFlag.value++
  nextTick(() => {
    console.log('畫面已強制更新')
  })
}

const forceUpdateList = () => {
  // 觸發重新渲染
  forceUpdateFlag.value++
}

// 獲取普通變數的實際值 (用於顯示實際值)
const getNormalCount = () => {
  forceUpdateFlag.value // 依賴這個響應式變數來觸發更新
  return normalCount
}

const getNormalUser = () => {
  forceUpdateFlag.value
  return { ...normalUser }
}

const getNormalItems = () => {
  forceUpdateFlag.value
  return [...normalItems]
}
</script>

<style scoped>
.without-reactivity-demo {
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
  border-bottom: 3px solid #e74c3c;
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

.normal-item {
  border-left: 5px solid #e74c3c;
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

.btn-danger {
  background: linear-gradient(135deg, #e74c3c, #c0392b);
  color: white;
}

.btn-danger:hover {
  background: linear-gradient(135deg, #c0392b, #a93226);
  transform: translateY(-2px);
}

.btn-warning {
  background: linear-gradient(135deg, #f39c12, #e67e22);
  color: white;
}

.btn-warning:hover {
  background: linear-gradient(135deg, #e67e22, #d35400);
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

.btn-small {
  padding: 4px 8px;
  font-size: 12px;
  background: #dc3545;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.btn-small:hover {
  background: #c82333;
}

/* 結果顯示 */
.result {
  margin-bottom: 20px;
  padding: 15px;
  background: #f8f9fa;
  border-radius: 8px;
  border: 1px solid #e9ecef;
  flex: 1;
  /* 讓結果區塊填滿可用空間 */
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
  border-radius: 6px;
  font-size: 14px;
  font-weight: 500;
}

.normal-item .note {
  background: #f8d7da;
  border: 1px solid #f5c6cb;
  color: #721c24;
}

.reactive-item .note {
  background: #d4edda;
  border: 1px solid #c3e6cb;
  color: #155724;
}

/* 項目列表 */
.item-list {
  margin: 15px 0;
  max-height: 200px;
  overflow-y: auto;
}

.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 8px 12px;
  margin-bottom: 5px;
  border-radius: 6px;
  font-size: 14px;
}

.item.warning {
  background: #fef9e7;
  border: 1px solid #ffeaa7;
  color: #856404;
}

.item.success {
  background: #eafaf1;
  border: 1px solid #c3e6cb;
  color: #155724;
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

/* 總結表格 */
.summary-table {
  background: white;
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

.table-header {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  background: linear-gradient(135deg, #2c3e50, #34495e);
  color: white;
  font-weight: 600;
  font-size: 16px;
}

.table-header span {
  padding: 20px;
  text-align: center;
  border-right: 1px solid rgba(255, 255, 255, 0.1);
}

.table-header span:last-child {
  border-right: none;
}

.table-row {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  border-bottom: 1px solid #e9ecef;
}

.table-row:last-child {
  border-bottom: none;
}

.table-row span {
  padding: 15px 20px;
  text-align: center;
  border-right: 1px solid #e9ecef;
  display: flex;
  align-items: center;
  justify-content: center;
}

.table-row span:first-child {
  font-weight: 600;
  background: #f8f9fa;
  color: #2c3e50;
}

.table-row span:last-child {
  border-right: none;
}

.normal-cell {
  background: #fef9e7;
  color: #856404;
  font-weight: 500;
}

.reactive-cell {
  background: #eafaf1;
  color: #155724;
  font-weight: 500;
}

/* 響應式設計 */
@media (max-width: 768px) {
  .without-reactivity-demo {
    padding: 15px;
  }

  .comparison-grid {
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

  .table-header,
  .table-row {
    grid-template-columns: 1fr;
  }

  .table-header span,
  .table-row span {
    border-right: none;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  }

  .table-row span {
    border-bottom: 1px solid #e9ecef;
  }

  .table-row span:first-child {
    font-size: 16px;
    font-weight: 700;
  }
}

@media (max-width: 480px) {
  .demo-section h3 {
    font-size: 20px;
  }

  .comparison-item {
    padding: 20px;
  }

  .route-info {
    font-size: 12px;
    padding: 6px 12px;
  }

  .table-header span,
  .table-row span {
    padding: 12px 15px;
    font-size: 14px;
  }
}
</style>
