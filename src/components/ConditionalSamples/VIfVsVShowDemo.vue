<template>
  <div class="vif-vs-vshow-demo">
    <h2>v-if vs v-show 性能對比</h2>
    <p class="route-info">📍 路徑：/ConditionalSamples/VIfVsVShowDemo.vue</p>
    <p class="description">理解兩者的差異和適用場景</p>

    <!-- 基本差異展示 -->
    <div class="demo-section">
      <h3>1. 基本差異展示</h3>
      <div class="controls">
        <button @click="toggleVisibility" class="btn btn-primary">
          切換顯示狀態 (當前: {{ isVisible ? '顯示' : '隱藏' }})
        </button>
      </div>

      <div class="comparison-grid">
        <div class="comparison-item">
          <h4>使用 v-if</h4>
          <div class="demo-box">
            <div v-if="isVisible" class="content-box vif-box">
              <h5>v-if 內容</h5>
              <p>我會被完全創建/銷毀</p>
              <span class="creation-time">創建時間: {{ vifCreationTime }}</span>
            </div>
            <div v-else class="placeholder">
              v-if 元素已被銷毀
            </div>
          </div>
          <div class="code-example">
            <pre v-pre><code>&lt;div v-if="isVisible"&gt;
  內容會被創建/銷毀
&lt;/div&gt;</code></pre>
          </div>
        </div>

        <div class="comparison-item">
          <h4>使用 v-show</h4>
          <div class="demo-box">
            <div v-show="isVisible" class="content-box vshow-box">
              <h5>v-show 內容</h5>
              <p>我只是被隱藏/顯示</p>
              <span class="creation-time">創建時間: {{ vshowCreationTime }}</span>
            </div>
          </div>
          <div class="code-example">
            <pre v-pre><code>&lt;div v-show="isVisible"&gt;
  內容始終存在，只改變 display
&lt;/div&gt;</code></pre>
          </div>
        </div>
      </div>
    </div>

    <!-- 性能測試 -->
    <div class="demo-section">
      <h3>2. 性能測試對比</h3>

      <div class="test-explanation">
        <h4>🔬 測試說明</h4>
        <ul>
          <li><strong>初始渲染</strong>：測試首次創建和渲染元素的時間</li>
          <li><strong>隱藏元素</strong>：測試隱藏元素的時間（v-if 銷毀 DOM，v-show 設置 display:none）</li>
          <li><strong>顯示元素</strong>：測試顯示元素的時間（v-if 重新創建 DOM，v-show 移除 display:none）</li>
          <li><strong>連續切換</strong>：測試頻繁切換時的性能表現</li>
        </ul>
        <p class="note">💡 <strong>預期結果</strong>：v-if 在初始渲染時可能更快（條件為 false 時），但切換時較慢；v-show 初始渲染較慢，但切換時更快。</p>
      </div>

      <div class="controls">
        <div class="control-group">
          <label>測試項目數量:</label>
          <select v-model="testItemCount" class="select-input">
            <option value="100">100 項目</option>
            <option value="500">500 項目</option>
            <option value="1000">1000 項目</option>
            <option value="2000">2000 項目</option>
          </select>
        </div>
        <div class="control-group">
          <button @click="runPerformanceTest('vif')" class="btn btn-danger">
            測試 v-if 性能
          </button>
          <button @click="runPerformanceTest('vshow')" class="btn btn-success">
            測試 v-show 性能
          </button>
          <button @click="startContinuousToggle" class="btn btn-warning" :disabled="isContinuousToggling">
            {{ isContinuousToggling ? `連續切換中... (${toggleCount}/100)` : '開始連續切換測試' }}
          </button>
        </div>
      </div>

      <div class="performance-results" v-if="performanceResults.length">
        <h4>📊 性能測試結果</h4>
        <div class="results-table">
          <div class="result-header">
            <span>測試類型</span>
            <span>項目數量</span>
            <span>耗時 (ms)</span>
            <span>操作</span>
          </div>
          <div v-for="result in performanceResults" :key="result.id" class="result-row" :class="result.type">
            <span>{{ result.type === 'vif' ? 'v-if' : result.type === 'vshow' ? 'v-show' : '連續切換' }}</span>
            <span>{{ result.itemCount }}</span>
            <span class="time-value">{{ result.time }}</span>
            <span>{{ result.operation }}</span>
          </div>
        </div>
        <button @click="clearResults" class="btn btn-secondary">清空結果</button>
      </div>

      <!-- 測試內容區域 -->
      <div class="test-content">
        <!-- v-if 測試區域 -->
        <div class="test-section" v-if="showVifTest">
          <h4>v-if 測試區域 ({{ visibleVifItems.length }}/{{ vifTestItems.length }} 項目)</h4>
          <div class="test-items">
            <div v-for="item in visibleVifItems" :key="item.id" class="test-item vif-item">
              <span>項目 {{ item.id }}</span>
              <div class="item-content">{{ item.content }}</div>
            </div>
          </div>
        </div>

        <!-- v-show 測試區域 -->
        <div class="test-section" v-if="showVshowTest">
          <h4>v-show 測試區域 ({{ vshowTestItems.length }} 項目)</h4>
          <div class="test-items">
            <div v-for="item in vshowTestItems" :key="item.id" v-show="item.visible" class="test-item vshow-item">
              <span>項目 {{ item.id }}</span>
              <div class="item-content">{{ item.content }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- 適用場景指南 -->
    <div class="demo-section">
      <h3>3. 適用場景指南</h3>
      <div class="scenario-grid">
        <div class="scenario-card vif-card">
          <h4>🔄 使用 v-if 的場景</h4>
          <ul>
            <li><strong>條件很少改變</strong> - 登入狀態、權限檢查</li>
            <li><strong>條件性載入</strong> - 根據路由顯示不同組件</li>
            <li><strong>節省記憶體</strong> - 大型組件的條件渲染</li>
            <li><strong>懶載入</strong> - 需要時才創建的內容</li>
          </ul>
          <div class="example">
            <h5>範例：用戶權限</h5>
            <div class="scenario-demo">
              <label class="checkbox-label">
                <input type="checkbox" v-model="hasAdminPermission">
                管理員權限
              </label>
              <div v-if="hasAdminPermission" class="admin-panel">
                <h6>🔧 管理員面板</h6>
                <p>這是只有管理員才能看到的內容</p>
                <button class="btn btn-sm">管理用戶</button>
                <button class="btn btn-sm">系統設定</button>
              </div>
            </div>
          </div>
        </div>

        <div class="scenario-card vshow-card">
          <h4>👁️ 使用 v-show 的場景</h4>
          <ul>
            <li><strong>頻繁切換</strong> - 標籤頁、摺疊面板</li>
            <li><strong>動畫效果</strong> - 需要 CSS 過渡動畫</li>
            <li><strong>表單驗證</strong> - 錯誤訊息的顯示隱藏</li>
            <li><strong>即時反饋</strong> - 搜尋結果、篩選器</li>
          </ul>
          <div class="example">
            <h5>範例：標籤頁切換</h5>
            <div class="scenario-demo">
              <div class="tab-buttons">
                <button v-for="tab in tabs" :key="tab.id" @click="activeTab = tab.id"
                  :class="['tab-btn', { active: activeTab === tab.id }]">
                  {{ tab.name }}
                </button>
              </div>
              <div class="tab-content">
                <div v-for="tab in tabs" :key="tab.id" v-show="activeTab === tab.id" class="tab-panel">
                  <h6>{{ tab.name }} 內容</h6>
                  <p>{{ tab.content }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- 總結對比 -->
    <div class="summary-section">
      <h3>📋 總結對比</h3>
      <div class="comparison-table">
        <div class="table-header">
          <span>特性</span>
          <span>v-if</span>
          <span>v-show</span>
        </div>
        <div class="table-row">
          <span>DOM 操作</span>
          <span class="vif-cell">創建/銷毀元素</span>
          <span class="vshow-cell">切換 display 屬性</span>
        </div>
        <div class="table-row">
          <span>初始渲染</span>
          <span class="vif-cell">條件為 false 時不渲染</span>
          <span class="vshow-cell">總是會渲染</span>
        </div>
        <div class="table-row">
          <span>切換開銷</span>
          <span class="vif-cell">較高</span>
          <span class="vshow-cell">較低</span>
        </div>
        <div class="table-row">
          <span>記憶體使用</span>
          <span class="vif-cell">動態變化</span>
          <span class="vshow-cell">固定佔用</span>
        </div>
        <div class="table-row">
          <span>CSS 動畫</span>
          <span class="vif-cell">不支援</span>
          <span class="vshow-cell">支援</span>
        </div>
        <div class="table-row">
          <span>適用場景</span>
          <span class="vif-cell">條件很少改變</span>
          <span class="vshow-cell">需要頻繁切換</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted, nextTick } from 'vue'

// 基本顯示控制
const isVisible = ref(true)
const vifCreationTime = ref('')
const vshowCreationTime = ref('')

// 性能測試
const testItemCount = ref(500)
const performanceResults = ref([])
const showVifTest = ref(false)
const showVshowTest = ref(false)
const vifTestItems = ref([])
const vshowTestItems = ref([])
const isContinuousToggling = ref(false)
let toggleInterval = null

// 場景示例
const hasAdminPermission = ref(false)
const activeTab = ref('tab1')
const tabs = ref([
  { id: 'tab1', name: '首頁', content: '這是首頁的內容，包含網站的主要資訊和導航。' },
  { id: 'tab2', name: '產品', content: '這是產品頁面，展示我們的各種產品和服務。' },
  { id: 'tab3', name: '關於', content: '這是關於我們的頁面，介紹公司的歷史和團隊。' }
])

// 切換顯示狀態
const toggleVisibility = () => {
  isVisible.value = !isVisible.value
  if (isVisible.value) {
    vifCreationTime.value = new Date().toLocaleTimeString()
  }
}

// 生成測試數據
const generateTestItems = (count) => {
  return Array.from({ length: count }, (_, i) => ({
    id: i + 1,
    visible: true,
    content: `這是測試內容 ${i + 1}，包含一些文字來模擬真實場景。`
  }))
}

// 性能測試
const runPerformanceTest = async (type) => {
  const count = parseInt(testItemCount.value)

  if (type === 'vif') {
    await testVifPerformance(count)
  } else {
    await testVshowPerformance(count)
  }
}

// v-if 性能測試
const testVifPerformance = async (count) => {
  // 測試初始渲染性能
  showVifTest.value = false
  vifTestItems.value = generateTestItems(count)

  const renderStartTime = performance.now()
  showVifTest.value = true
  await nextTick()
  const renderEndTime = performance.now()

  performanceResults.value.push({
    id: Date.now(),
    type: 'vif',
    itemCount: count,
    time: Math.round(renderEndTime - renderStartTime),
    operation: '初始渲染'
  })

  // 測試切換性能（隱藏）
  const hideStartTime = performance.now()
  vifTestItems.value.forEach(item => item.visible = false)
  await nextTick()
  const hideEndTime = performance.now()

  performanceResults.value.push({
    id: Date.now() + 1,
    type: 'vif',
    itemCount: count,
    time: Math.round(hideEndTime - hideStartTime),
    operation: '隱藏元素'
  })

  // 測試切換性能（顯示）
  const showStartTime = performance.now()
  vifTestItems.value.forEach(item => item.visible = true)
  await nextTick()
  const showEndTime = performance.now()

  performanceResults.value.push({
    id: Date.now() + 2,
    type: 'vif',
    itemCount: count,
    time: Math.round(showEndTime - showStartTime),
    operation: '顯示元素'
  })
}

// v-show 性能測試
const testVshowPerformance = async (count) => {
  // 測試初始渲染性能
  showVshowTest.value = false
  vshowTestItems.value = generateTestItems(count)

  const renderStartTime = performance.now()
  showVshowTest.value = true
  await nextTick()
  const renderEndTime = performance.now()

  performanceResults.value.push({
    id: Date.now(),
    type: 'vshow',
    itemCount: count,
    time: Math.round(renderEndTime - renderStartTime),
    operation: '初始渲染'
  })

  // 測試切換性能（隱藏）
  const hideStartTime = performance.now()
  vshowTestItems.value.forEach(item => item.visible = false)
  await nextTick()
  const hideEndTime = performance.now()

  performanceResults.value.push({
    id: Date.now() + 1,
    type: 'vshow',
    itemCount: count,
    time: Math.round(hideEndTime - hideStartTime),
    operation: '隱藏元素'
  })

  // 測試切換性能（顯示）
  const showStartTime = performance.now()
  vshowTestItems.value.forEach(item => item.visible = true)
  await nextTick()
  const showEndTime = performance.now()

  performanceResults.value.push({
    id: Date.now() + 2,
    type: 'vshow',
    itemCount: count,
    time: Math.round(showEndTime - showStartTime),
    operation: '顯示元素'
  })
}

// 連續切換測試
const toggleCount = ref(0)
const startContinuousToggle = () => {
  if (isContinuousToggling.value) {
    clearInterval(toggleInterval)
    isContinuousToggling.value = false

    // 記錄連續切換測試結果
    performanceResults.value.push({
      id: Date.now(),
      type: 'continuous',
      itemCount: 100,
      time: toggleCount.value,
      operation: `連續切換 ${toggleCount.value} 次`
    })

    toggleCount.value = 0
    return
  }

  isContinuousToggling.value = true
  toggleCount.value = 0
  let isVifVisible = true
  let isVshowVisible = true

  // 準備測試數據
  vifTestItems.value = generateTestItems(100)
  vshowTestItems.value = generateTestItems(100)
  showVifTest.value = true
  showVshowTest.value = true

  toggleInterval = setInterval(() => {
    const startTime = performance.now()

    isVifVisible = !isVifVisible
    isVshowVisible = !isVshowVisible

    vifTestItems.value.forEach(item => item.visible = isVifVisible)
    vshowTestItems.value.forEach(item => item.visible = isVshowVisible)

    toggleCount.value++

    const endTime = performance.now()
    const duration = endTime - startTime

    // 每10次切換記錄一次性能數據
    if (toggleCount.value % 10 === 0) {
      performanceResults.value.push({
        id: Date.now() + Math.random(),
        type: 'toggle-batch',
        itemCount: 100,
        time: Math.round(duration),
        operation: `第 ${toggleCount.value} 次切換`
      })
    }

    // 自動停止在100次切換後
    if (toggleCount.value >= 100) {
      clearInterval(toggleInterval)
      isContinuousToggling.value = false

      performanceResults.value.push({
        id: Date.now(),
        type: 'continuous-summary',
        itemCount: 100,
        time: toggleCount.value,
        operation: '連續切換測試完成'
      })
    }
  }, 100) // 減少間隔時間以更快地測試
}

// 清空結果
const clearResults = () => {
  performanceResults.value = []
  showVifTest.value = false
  showVshowTest.value = false
  vifTestItems.value = []
  vshowTestItems.value = []
}

// 初始化
onMounted(() => {
  vifCreationTime.value = new Date().toLocaleTimeString()
  vshowCreationTime.value = new Date().toLocaleTimeString()
})

// 清理
onUnmounted(() => {
  if (toggleInterval) {
    clearInterval(toggleInterval)
  }
})

// 計算 visibleVifItems
const visibleVifItems = computed(() => {
  return vifTestItems.value.filter(item => item.visible)
})
</script>
