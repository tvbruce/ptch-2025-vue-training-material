<!-- components/LifecycleSamples/BasicLifecycleDemo.vue -->
<template>
  <div class="basic-lifecycle-demo">
    <h2>基本生命週期鉤子</h2>
    <p class="route-info">📍 路徑：/LifecycleSamples/BasicLifecycleDemo.vue</p>

    <!-- 生命週期日誌 -->
    <div class="demo-section">
      <h3>1. 生命週期執行記錄</h3>
      <div class="controls">
        <button @click="clearLogs" class="btn btn-secondary">
          清除記錄
        </button>
        <button @click="triggerUpdate" class="btn btn-primary">
          手動觸發更新
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
      <div class="code-example">
        <pre v-pre><code>// 基本生命週期鉤子
import { ref, onMounted, onUpdated, onUnmounted, nextTick } from 'vue'

const lifecycleLogs = ref([])

const addLog = (hook, message, type = 'info') => {
  lifecycleLogs.value.push({
    time: new Date().toLocaleTimeString(),
    hook,
    message,
    type
  })
}

// 組件掛載完成
onMounted(() => {
  addLog('onMounted', '組件已掛載到 DOM', 'success')
})

// 組件更新後 - 使用 nextTick 避免無限遞歸
onUpdated(() => {
  // 使用 nextTick 確保在下一個 tick 中執行，避免無限遞歸
  nextTick(() => {
    console.log('組件已更新')
  })
})

// 組件卸載前
onUnmounted(() => {
  addLog('onUnmounted', '組件即將卸載', 'error')
})</code></pre>
      </div>
    </div>

    <!-- 數據變化觀察 -->
    <div class="demo-section">
      <h3>2. 數據變化與生命週期</h3>
      <div class="controls">
        <input v-model="message" placeholder="輸入訊息" class="input-field">
        <input v-model.number="counter" type="number" placeholder="數字" class="input-field">
      </div>
      <div class="result">
        <div class="data-display">
          <div class="data-item">
            <label>目前訊息：</label>
            <span class="data-value">{{ message }}</span>
          </div>
          <div class="data-item">
            <label>計數器：</label>
            <span class="data-value">{{ counter }}</span>
          </div>
          <div class="data-item">
            <label>手動更新次數：</label>
            <span class="data-value">{{ manualUpdateCount }}</span>
          </div>
        </div>
        <div class="info-box">
          <p><strong>觀察：</strong>修改上方輸入框的值會觸發組件重新渲染，但我們不在 onUpdated 中修改響應式數據以避免無限遞歸</p>
        </div>
      </div>
    </div>

    <!-- 組件狀態 -->
    <div class="demo-section">
      <h3>3. 組件狀態追蹤</h3>
      <div class="controls">
        <button @click="toggleChildComponent" class="btn btn-warning">
          {{ showChild ? '隱藏' : '顯示' }} 子組件
        </button>
      </div>
      <div class="result">
        <div class="component-status">
          <div class="status-item">
            <span>主組件狀態：</span>
            <span class="status-active">已掛載</span>
          </div>
          <div class="status-item">
            <span>子組件狀態：</span>
            <span :class="showChild ? 'status-active' : 'status-inactive'">
              {{ showChild ? '已掛載' : '未掛載' }}
            </span>
          </div>
        </div>

        <div class="child-component-area">
          <ChildComponent v-if="showChild" @lifecycle-event="handleChildEvent" />
          <div v-else class="no-child">
            子組件未顯示
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 子組件生命週期
&lt;template&gt;
  &lt;ChildComponent v-if="showChild" @lifecycle-event="handleChildEvent" /&gt;
&lt;/template&gt;

// 當 showChild 從 true 變為 false 時：
// 子組件會觸發 onUnmounted 鉤子

// 當 showChild 從 false 變為 true 時：
// 子組件會觸發 onMounted 鉤子</code></pre>
      </div>
    </div>

    <!-- 生命週期時機演示 -->
    <div class="demo-section">
      <h3>4. 生命週期時機演示</h3>
      <div class="controls">
        <button @click="addListItem" class="btn btn-success">
          添加列表項目
        </button>
        <button @click="removeLastItem" class="btn btn-danger">
          移除最後項目
        </button>
      </div>
      <div class="result">
        <div class="list-demo">
          <div v-for="item in listItems" :key="item.id" class="list-item">
            {{ item.text }} (ID: {{ item.id }})
          </div>
          <div v-if="listItems.length === 0" class="empty-list">
            列表為空
          </div>
        </div>
        <div class="info-box">
          <p><strong>說明：</strong>添加或移除列表項目會觸發組件更新，但不會造成無限遞歸</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUpdated, onUnmounted, nextTick } from 'vue'
import ChildComponent from './ChildComponent.vue'

// 生命週期日誌
const lifecycleLogs = ref([])
const manualUpdateCount = ref(0)

const addLog = (hook, message, type = 'info') => {
  lifecycleLogs.value.push({
    time: new Date().toLocaleTimeString(),
    hook,
    message,
    type
  })
}

// 數據
const message = ref('Hello Vue')
const counter = ref(0)
const showChild = ref(false)
const listItems = ref([])

// 生命週期鉤子
onMounted(() => {
  addLog('onMounted', '主組件已掛載到 DOM', 'success')
})

// 修正：使用 nextTick 避免在 onUpdated 中直接修改響應式數據
onUpdated(() => {
  // 使用 nextTick 確保在下一個 tick 中執行，避免無限遞歸
  nextTick(() => {
    console.log('組件已更新，但不在此處修改響應式數據')
  })
})

onUnmounted(() => {
  addLog('onUnmounted', '主組件即將卸載', 'error')
})

// 方法
const clearLogs = () => {
  lifecycleLogs.value = []
  manualUpdateCount.value = 0
}

const triggerUpdate = () => {
  // 手動觸發更新，這是安全的方式
  manualUpdateCount.value++
  addLog('Manual Update', `手動觸發更新 (第 ${manualUpdateCount.value} 次)`, 'info')
}

const toggleChildComponent = () => {
  showChild.value = !showChild.value
}

const handleChildEvent = (eventData) => {
  addLog(eventData.hook, `子組件: ${eventData.message}`, eventData.type)
}

const addListItem = () => {
  const id = Date.now()
  listItems.value.push({
    id,
    text: `項目 ${listItems.value.length + 1}`
  })
}

const removeLastItem = () => {
  if (listItems.value.length > 0) {
    listItems.value.pop()
  }
}
</script>

<style scoped>
/* 樣式已在 src/assets/main.css 中定義 */
</style>
