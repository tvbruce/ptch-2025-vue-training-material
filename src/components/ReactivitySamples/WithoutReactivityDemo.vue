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
