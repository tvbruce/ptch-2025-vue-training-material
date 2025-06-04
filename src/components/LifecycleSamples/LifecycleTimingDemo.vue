<!-- components/LifecycleSamples/LifecycleTimingDemo.vue -->
<template>
  <div class="lifecycle-timing-demo">
    <h2>生命週期執行時機</h2>
    <p class="route-info">📍 路徑：/LifecycleSamples/LifecycleTimingDemo.vue</p>

    <!-- DOM 訪問時機 -->
    <div class="demo-section">
      <h3>1. DOM 元素訪問時機</h3>
      <div class="controls">
        <button @click="checkDOMAccess" class="btn btn-primary">
          檢查 DOM 訪問
        </button>
        <button @click="updateContent" class="btn btn-secondary">
          更新內容
        </button>
      </div>
      <div class="result">
        <div ref="contentElement" class="content-element">
          {{ content }}
        </div>
        <div class="dom-info">
          <div class="info-item">
            <span>元素寬度：</span>
            <span>{{ elementWidth }}px</span>
          </div>
          <div class="info-item">
            <span>元素高度：</span>
            <span>{{ elementHeight }}px</span>
          </div>
          <div class="info-item">
            <span>檢查時機：</span>
            <span>{{ checkTiming }}</span>
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// DOM 訪問時機
import { ref, onMounted, nextTick } from 'vue'

const contentElement = ref(null)

onMounted(() => {
  // ✅ 在 onMounted 中可以安全訪問 DOM
  console.log(contentElement.value) // 有值
  const rect = contentElement.value.getBoundingClientRect()
})

const updateContent = async () => {
  content.value = '新內容'

  // ❌ DOM 還沒更新
  console.log('立即檢查:', contentElement.value.textContent)

  // ✅ 等待 DOM 更新
  await nextTick()
  console.log('nextTick 後:', contentElement.value.textContent)
}</code></pre>
      </div>
    </div>

    <!-- nextTick 演示 -->
    <div class="demo-section">
      <h3>2. nextTick 使用時機</h3>
      <div class="controls">
        <input v-model="userInput" placeholder="輸入文字觀察變化" class="input-field">
        <button @click="demonstrateNextTick" class="btn btn-warning">
          演示 nextTick
        </button>
      </div>
      <div class="result">
        <div class="timing-display">
          <div class="timing-item">
            <h4>響應式數據</h4>
            <div class="data-value">{{ userInput || '請輸入文字' }}</div>
          </div>

          <div class="timing-item">
            <h4>DOM 內容</h4>
            <div ref="displayElement" class="data-value">{{ userInput || '請輸入文字' }}</div>
          </div>
        </div>

        <div class="timing-logs">
          <h4>執行順序記錄：</h4>
          <div class="log-list">
            <div v-for="(log, index) in timingLogs" :key="index" class="timing-log">
              {{ log }}
            </div>
            <div v-if="timingLogs.length === 0" class="no-logs">
              點擊「演示 nextTick」或修改輸入框來查看執行順序
            </div>
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// nextTick 使用演示
import { ref, nextTick } from 'vue'

const userInput = ref('')
const displayElement = ref(null)

const demonstrateNextTick = async () => {
  const oldValue = userInput.value
  userInput.value = `新值 ${Date.now()}`

  // 立即檢查 DOM (還沒更新)
  console.log('立即檢查:', displayElement.value.textContent)

  // 等待 DOM 更新
  await nextTick()
  console.log('nextTick 後:', displayElement.value.textContent)
}</code></pre>
      </div>
    </div>

    <!-- 異步操作時機 -->
    <div class="demo-section">
      <h3>3. 異步操作最佳時機</h3>
      <div class="controls">
        <button @click="loadData" class="btn btn-success" :disabled="loading">
          {{ loading ? '載入中...' : '載入數據' }}
        </button>
        <button @click="clearData" class="btn btn-secondary">
          清除數據
        </button>
      </div>
      <div class="result">
        <div class="async-status">
          <div class="status-item">
            <span>載入狀態：</span>
            <span :class="loading ? 'status-loading' : 'status-ready'">
              {{ loading ? '載入中' : '就緒' }}
            </span>
          </div>
          <div class="status-item">
            <span>數據筆數：</span>
            <span>{{ asyncData.length }}</span>
          </div>
        </div>

        <div class="async-data">
          <div v-if="loading" class="loading-spinner">
            載入中...
          </div>
          <div v-else-if="asyncData.length > 0" class="data-list">
            <div v-for="item in asyncData" :key="item.id" class="data-item">
              <span>{{ item.name }}</span>
              <span class="item-value">{{ item.value }}</span>
            </div>
          </div>
          <div v-else class="no-data">
            點擊「載入數據」開始
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 異步操作時機
import { ref, onMounted } from 'vue'

const loading = ref(false)
const asyncData = ref([])

// ✅ 在 onMounted 中執行初始化異步操作
onMounted(async () => {
  try {
    loading.value = true
    const data = await fetchInitialData()
    asyncData.value = data
  } catch (error) {
    console.error('載入失敗:', error)
  } finally {
    loading.value = false
  }
})

const loadData = async () => {
  loading.value = true
  addLifecycleLog('Async Start', '開始異步載入數據', 'warning')

  try {
    // 模擬 API 延遲
    await new Promise(resolve => setTimeout(resolve, 1500))

    asyncData.value = [
      { id: 1, name: '用戶數據', value: Math.floor(Math.random() * 1000) },
      { id: 2, name: '訂單數量', value: Math.floor(Math.random() * 500) },
      { id: 3, name: '收入金額', value: (Math.random() * 10000).toFixed(2) },
      { id: 4, name: '活躍用戶', value: Math.floor(Math.random() * 800) }
    ]

    addLifecycleLog('Async Success', `成功載入 ${asyncData.value.length} 筆數據`, 'success')
  } catch (error) {
    console.error('載入失敗:', error)
    addLifecycleLog('Async Error', '數據載入失敗', 'error')
  } finally {
    loading.value = false
  }
}

const clearData = () => {
  asyncData.value = []
  timingLogs.value = []
  addLifecycleLog('Clear Data', '清除所有數據', 'info')
}
</code></pre>
      </div>
    </div>

    <!-- 生命週期記錄 -->
    <div class="demo-section">
      <h3>4. 生命週期記錄</h3>
      <div class="controls">
        <button @click="clearLifecycleLogs" class="btn btn-secondary">
          清除記錄
        </button>
        <button @click="triggerManualUpdate" class="btn btn-info">
          手動觸發記錄
        </button>
      </div>
      <div class="result">
        <div class="lifecycle-logs">
          <div v-for="(log, index) in lifecycleLogs" :key="index" :class="['log-item', log.type]">
            <span class="log-time">{{ log.time }}</span>
            <span class="log-hook">{{ log.hook }}</span>
            <span class="log-message">{{ log.message }}</span>
          </div>
          <div v-if="lifecycleLogs.length === 0" class="no-logs">
            暫無記錄，重新載入頁面或執行操作來查看生命週期
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted, nextTick } from 'vue'

// DOM 訪問
const contentElement = ref(null)
const content = ref('這是初始內容')
const elementWidth = ref(0)
const elementHeight = ref(0)
const checkTiming = ref('未檢查')

// nextTick 演示
const userInput = ref('')
const displayElement = ref(null)
const timingLogs = ref([])

// 異步操作
const loading = ref(false)
const asyncData = ref([])

// 生命週期記錄
const lifecycleLogs = ref([])

const addLifecycleLog = (hook, message, type = 'info') => {
  lifecycleLogs.value.push({
    time: new Date().toLocaleTimeString(),
    hook,
    message,
    type
  })
}

// 生命週期鉤子
onMounted(() => {
  addLifecycleLog('onMounted', '組件已掛載，可以安全訪問 DOM', 'success')

  // DOM 訪問
  if (contentElement.value) {
    const rect = contentElement.value.getBoundingClientRect()
    elementWidth.value = Math.round(rect.width)
    elementHeight.value = Math.round(rect.height)
    checkTiming.value = 'onMounted'
  }
})

onUnmounted(() => {
  addLifecycleLog('onUnmounted', '組件即將卸載', 'error')
})

// 方法
const checkDOMAccess = () => {
  if (contentElement.value) {
    const rect = contentElement.value.getBoundingClientRect()
    elementWidth.value = Math.round(rect.width)
    elementHeight.value = Math.round(rect.height)
    checkTiming.value = '手動檢查'
    addLifecycleLog('Manual Check', 'DOM 元素手動檢查完成', 'info')
  }
}

const updateContent = async () => {
  const oldContent = content.value
  content.value = `更新時間: ${new Date().toLocaleTimeString()}`

  // 立即檢查 (DOM 還沒更新)
  checkTiming.value = '更新前'

  // 等待 DOM 更新
  await nextTick()
  checkTiming.value = 'nextTick 後'

  // 重新測量
  if (contentElement.value) {
    const rect = contentElement.value.getBoundingClientRect()
    elementWidth.value = Math.round(rect.width)
    elementHeight.value = Math.round(rect.height)
  }

  addLifecycleLog('Content Update', `內容從 "${oldContent}" 更新為 "${content.value}"`, 'warning')
}

const demonstrateNextTick = async () => {
  timingLogs.value = [] // 清除舊記錄

  const oldValue = userInput.value
  const newValue = `演示值 ${Date.now()}`

  timingLogs.value.push(`1. 準備更新數據: "${oldValue}" → "${newValue}"`)

  userInput.value = newValue

  // 立即檢查 DOM (還沒更新)
  if (displayElement.value) {
    timingLogs.value.push(`2. 立即檢查 DOM: "${displayElement.value.textContent}"`)
  }

  // 等待 DOM 更新
  await nextTick()

  if (displayElement.value) {
    timingLogs.value.push(`3. nextTick 後檢查 DOM: "${displayElement.value.textContent}"`)
  }

  addLifecycleLog('nextTick Demo', 'nextTick 演示完成', 'info')
}

const loadData = async () => {
  loading.value = true
  addLifecycleLog('Async Start', '開始異步載入數據', 'warning')

  try {
    // 模擬 API 延遲
    await new Promise(resolve => setTimeout(resolve, 1500))

    asyncData.value = [
      { id: 1, name: '用戶數據', value: Math.floor(Math.random() * 1000) },
      { id: 2, name: '訂單數量', value: Math.floor(Math.random() * 500) },
      { id: 3, name: '收入金額', value: (Math.random() * 10000).toFixed(2) },
      { id: 4, name: '活躍用戶', value: Math.floor(Math.random() * 800) }
    ]

    addLifecycleLog('Async Success', `成功載入 ${asyncData.value.length} 筆數據`, 'success')
  } catch (error) {
    console.error('載入失敗:', error)
    addLifecycleLog('Async Error', '數據載入失敗', 'error')
  } finally {
    loading.value = false
  }
}

const clearData = () => {
  asyncData.value = []
  timingLogs.value = []
  addLifecycleLog('Clear Data', '清除所有數據', 'info')
}

const clearLifecycleLogs = () => {
  lifecycleLogs.value = []
}

const triggerManualUpdate = () => {
  addLifecycleLog('Manual Trigger', '手動觸發記錄', 'info')
}
</script>

<style scoped>
/* 樣式已在 src/assets/main.css 中定義 */
</style>
