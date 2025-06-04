<template>
  <div class="list-rendering-demo">
    <h2>大數據列表性能優化</h2>
    <p class="route-info">📍 路徑：/ListSamples/PerformanceDemo.vue</p>
    <p class="description">
      當渲染大量數據時，不當的實現會導致明顯的性能問題和頁面卡頓
    </p>

    <div class="demo-section">
      <h3>性能對比測試 <span class="code-path">PerformanceDemo.vue</span></h3>
      <div class="demo-container">
        <!-- 錯誤示範：會造成卡頓 -->
        <div class="demo-panel">
          <h4>❌ 性能問題示範</h4>
          <div class="controls">
            <button @click="renderBadList(10000)" class="btn btn-danger">
              渲染 10,000 項目 (會卡頓)
            </button>
            <button @click="renderBadList(50000)" class="btn btn-danger">
              渲染 50,000 項目 (嚴重卡頓)
            </button>
            <button @click="clearBadList" class="btn btn-secondary">清空</button>
          </div>

          <div class="result">
            <div class="performance-info" v-if="badRenderTime">
              <span class="render-time">渲染耗時: {{ badRenderTime }}ms</span>
              <span class="item-count">項目數量: {{ badList.length }}</span>
            </div>

            <!-- 這裡會造成性能問題 -->
            <div class="bad-list" ref="badListRef">
              <div v-for="item in badList" :key="item.id" class="bad-item" :style="{
                backgroundColor: item.color,
                transform: `rotate(${item.rotation}deg)`,
                borderRadius: `${item.borderRadius}px`
              }">
                <div class="item-content">
                  <span class="item-name">{{ item.name }}</span>
                  <span class="item-value">值: {{ formatNumber(item.value) }}</span>
                  <span class="item-timestamp">{{ formatTime(item.timestamp) }}</span>
                  <div class="item-progress">
                    <div class="progress-bar" :style="{ width: item.progress + '%' }"></div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- 正確示範：使用虛擬滾動 -->
        <div class="demo-panel">
          <h4>✅ 虛擬滾動優化</h4>
          <div class="controls">
            <button @click="renderGoodList(10000)" class="btn btn-success">
              渲染 10,000 項目 (流暢)
            </button>
            <button @click="renderGoodList(100000)" class="btn btn-success">
              渲染 100,000 項目 (依然流暢)
            </button>
            <button @click="clearGoodList" class="btn btn-secondary">清空</button>
          </div>

          <div class="result">
            <div class="performance-info" v-if="goodRenderTime">
              <span class="render-time">渲染耗時: {{ goodRenderTime }}ms</span>
              <span class="item-count">項目數量: {{ goodList.length }}</span>
              <span class="visible-count">可見項目: {{ visibleItems.length }}</span>
            </div>

            <!-- 虛擬滾動實現 -->
            <div class="good-list" ref="goodListRef" @scroll="handleScroll">
              <div class="virtual-spacer-top" :style="{ height: topSpacerHeight + 'px' }"></div>

              <div v-for="item in visibleItems" :key="item.id" class="good-item" :style="{
                backgroundColor: item.color,
                transform: `rotate(${item.rotation}deg)`,
                borderRadius: `${item.borderRadius}px`
              }">
                <div class="item-content">
                  <span class="item-name">{{ item.name }}</span>
                  <span class="item-value">值: {{ formatNumber(item.value) }}</span>
                  <span class="item-timestamp">{{ formatTime(item.timestamp) }}</span>
                  <div class="item-progress">
                    <div class="progress-bar" :style="{ width: item.progress + '%' }"></div>
                  </div>
                </div>
              </div>

              <div class="virtual-spacer-bottom" :style="{ height: bottomSpacerHeight + 'px' }"></div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="demo-section">
      <h3>📊 性能監控 <span class="code-path">監控工具</span></h3>
      <div class="result">
        <!-- 性能監控 -->
        <div class="performance-monitor" v-if="isMonitoring">
          <h4>📊 性能監控</h4>
          <div class="monitor-grid">
            <div class="monitor-item">
              <span class="monitor-label">FPS:</span>
              <span class="monitor-value" :class="{ 'fps-low': currentFPS < 30 }">
                {{ currentFPS }}
              </span>
            </div>
            <div class="monitor-item">
              <span class="monitor-label">記憶體使用:</span>
              <span class="monitor-value">{{ memoryUsage }}MB</span>
            </div>
            <div class="monitor-item">
              <span class="monitor-label">DOM 節點:</span>
              <span class="monitor-value">{{ domNodeCount }}</span>
            </div>
          </div>
          <button @click="toggleMonitoring" class="btn btn-secondary">停止監控</button>
        </div>

        <div v-else class="performance-monitor">
          <button @click="toggleMonitoring" class="btn btn-primary">開始性能監控</button>
        </div>
      </div>
    </div>

    <div class="demo-section">
      <h3>🔍 測試指南 <span class="code-path">使用說明</span></h3>
      <div class="result">
        <div class="explanation">
          <h4>🔍 測試步驟：</h4>
          <ol>
            <li>先點擊「開始性能監控」觀察基準性能</li>
            <li>點擊左側「渲染 10,000 項目」，感受頁面卡頓</li>
            <li>嘗試滾動左側列表，觀察卡頓程度</li>
            <li>點擊右側「渲染 10,000 項目」，對比流暢度</li>
            <li>滾動右側列表，感受虛擬滾動的流暢性</li>
            <li>觀察性能監控中的 FPS 和記憶體變化</li>
          </ol>
        </div>
      </div>
    </div>

    <div class="demo-section">
      <h3>🚀 優化策略 <span class="code-path">最佳實踐</span></h3>
      <div class="result">
        <div class="optimization-strategies">
          <h4>🚀 性能優化策略：</h4>
          <div class="strategy-grid">
            <div class="strategy-item">
              <h5>1. 虛擬滾動</h5>
              <p>只渲染可見區域的項目，大幅減少 DOM 節點數量</p>
              <code>只渲染 ~20 個可見項目 vs 全部 50,000 個</code>
            </div>

            <div class="strategy-item">
              <h5>2. 分頁載入</h5>
              <p>分批載入數據，避免一次性渲染大量內容</p>
              <code>每頁 50-100 項目，按需載入</code>
            </div>

            <div class="strategy-item">
              <h5>3. v-memo 指令 (Vue 3.2+)</h5>
              <p>記憶化渲染結果，避免不必要的重新計算</p>
              <code>&lt;div v-memo="[item.id, item.value]"&gt;</code>
            </div>

            <div class="strategy-item">
              <h5>4. 計算屬性優化</h5>
              <p>避免在模板中進行複雜計算</p>
              <code>使用 computed 而非方法調用</code>
            </div>

            <div class="strategy-item">
              <h5>5. Object.freeze()</h5>
              <p>凍結不變的數據，減少響應式開銷</p>
              <code>Object.freeze(staticData)</code>
            </div>

            <div class="strategy-item">
              <h5>6. 延遲載入</h5>
              <p>使用 Intersection Observer 實現懶載入</p>
              <code>進入視窗時才載入內容</code>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, nextTick, onMounted, onUnmounted } from 'vue'

// 數據列表
const badList = ref([])
const goodList = ref([])

// 性能監控
const badRenderTime = ref(0)
const goodRenderTime = ref(0)
const isMonitoring = ref(false)
const currentFPS = ref(60)
const memoryUsage = ref(0)
const domNodeCount = ref(0)

// 虛擬滾動相關
const goodListRef = ref(null)
const itemHeight = 120 // 每個項目的高度
const containerHeight = 400 // 容器高度
const visibleCount = Math.ceil(containerHeight / itemHeight) + 2 // 可見項目數量 + 緩衝
const scrollTop = ref(0)

// 虛擬滾動計算
const startIndex = computed(() => {
  return Math.max(0, Math.floor(scrollTop.value / itemHeight) - 1)
})

const endIndex = computed(() => {
  return Math.min(goodList.value.length, startIndex.value + visibleCount)
})

const visibleItems = computed(() => {
  return goodList.value.slice(startIndex.value, endIndex.value)
})

const topSpacerHeight = computed(() => {
  return startIndex.value * itemHeight
})

const bottomSpacerHeight = computed(() => {
  return (goodList.value.length - endIndex.value) * itemHeight
})

// 生成測試數據
const generateTestData = (count) => {
  const items = []
  for (let i = 0; i < count; i++) {
    items.push({
      id: i,
      name: `項目 ${i.toLocaleString()}`,
      value: Math.floor(Math.random() * 1000000),
      timestamp: Date.now() + i * 1000,
      color: `hsl(${(i * 137.508) % 360}, 70%, 80%)`,
      rotation: Math.random() * 10 - 5,
      borderRadius: Math.random() * 20,
      progress: Math.random() * 100
    })
  }
  return items
}

// 渲染方法
const renderBadList = async (count) => {
  const startTime = performance.now()

  // 故意添加一些複雜計算來加重負擔
  const items = generateTestData(count)
  badList.value = items

  await nextTick()
  badRenderTime.value = Math.round(performance.now() - startTime)
}

const renderGoodList = async (count) => {
  const startTime = performance.now()

  const items = generateTestData(count)
  goodList.value = items
  scrollTop.value = 0

  await nextTick()
  goodRenderTime.value = Math.round(performance.now() - startTime)
}

const clearBadList = () => {
  badList.value = []
  badRenderTime.value = 0
}

const clearGoodList = () => {
  goodList.value = []
  goodRenderTime.value = 0
  scrollTop.value = 0
}

// 虛擬滾動處理
const handleScroll = (event) => {
  scrollTop.value = event.target.scrollTop
}

// 格式化方法
const formatNumber = (num) => {
  return num.toLocaleString()
}

const formatTime = (timestamp) => {
  return new Date(timestamp).toLocaleTimeString()
}

// 性能監控
let fpsCounter = 0
let lastTime = performance.now()
let monitoringInterval = null

const updatePerformanceMetrics = () => {
  // FPS 計算
  const now = performance.now()
  fpsCounter++

  if (now - lastTime >= 1000) {
    currentFPS.value = Math.round(fpsCounter * 1000 / (now - lastTime))
    fpsCounter = 0
    lastTime = now
  }

  // 記憶體使用 (如果可用)
  if (performance.memory) {
    memoryUsage.value = Math.round(performance.memory.usedJSHeapSize / 1024 / 1024)
  }

  // DOM 節點計數
  domNodeCount.value = document.querySelectorAll('*').length
}

const toggleMonitoring = () => {
  isMonitoring.value = !isMonitoring.value

  if (isMonitoring.value) {
    monitoringInterval = setInterval(updatePerformanceMetrics, 100)
  } else {
    clearInterval(monitoringInterval)
  }
}

// 組件卸載時清理
onUnmounted(() => {
  if (monitoringInterval) {
    clearInterval(monitoringInterval)
  }
})

// 初始化時開始監控
onMounted(() => {
  toggleMonitoring()
})
</script>
