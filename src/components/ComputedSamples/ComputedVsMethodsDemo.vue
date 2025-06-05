<!-- components/ComputedSamples/ComputedVsMethodsDemo.vue -->
<template>
  <div class="computed-vs-methods-demo">
    <h2>計算屬性 vs 方法比較</h2>
    <p class="route-info">📍 路徑：/ComputedSamples/ComputedVsMethodsDemo.vue</p>

    <!-- 快取機制比較 -->
    <div class="demo-section">
      <h3>1. 快取機制比較</h3>
      <div class="controls">
        <input v-model="message" placeholder="輸入訊息" class="input-field">
        <button @click="forceUpdate" class="btn btn-primary">
          強制重新渲染
        </button>
      </div>
      <div class="result" :key="forceUpdateKey">
        <div class="comparison-grid">
          <div class="comparison-item">
            <h4>計算屬性 (有快取)</h4>
            <div class="value-display">
              <span>反轉訊息：</span>
              <span class="computed-value">{{ reversedMessageComputed }}</span>
            </div>
            <div class="call-count">
              計算次數：{{ computedCallCount }}
            </div>
            <div class="render-count">
              渲染次數：{{ forceUpdateKey }}
            </div>
          </div>

          <div class="comparison-item">
            <h4>方法 (無快取)</h4>
            <div class="value-display">
              <span>反轉訊息：</span>
              <span class="method-value">{{ methodResult }}</span>
            </div>
            <div class="call-count">
              呼叫次數：{{ methodCallCount }}
            </div>
            <button @click="callMethod" class="btn btn-small">
              手動呼叫方法
            </button>
          </div>
        </div>

        <div class="explanation">
          <p><strong>說明：</strong></p>
          <ul>
            <li>計算屬性：基於響應式依賴的快取，只有當 message 改變時才會重新計算</li>
            <li>方法：每次呼叫都會執行，沒有快取機制</li>
            <li>點擊「強制重新渲染」按鈕會重新渲染組件，觀察計算次數變化</li>
            <li>計算屬性在相同輸入下會使用快取結果，而方法每次都重新執行</li>
          </ul>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 計算屬性 - 有快取
const reversedMessageComputed = computed(() => {
  return message.value.split('').reverse().join('')
})

// 監聽計算屬性的變化來追蹤計算次數
watch(reversedMessageComputed, () => {
  computedCallCount.value++
}, { immediate: true })

// 方法 - 無快取
const reversedMessageMethod = () => {
  methodCallCount.value++
  return message.value.split('').reverse().join('')
}

const callMethod = () => {
  methodResult.value = reversedMessageMethod()
}</code></pre>
      </div>
    </div>

    <!-- 使用時機 -->
    <div class="demo-section">
      <h3>2. 使用時機範例</h3>
      <div class="controls">
        <input v-model.number="listSize" type="number" min="1" max="1000" placeholder="列表大小" class="input-field">
        <input v-model="filterText" placeholder="過濾文字" class="input-field">
        <button @click="addRandomItem" class="btn btn-secondary">
          添加隨機項目
        </button>
      </div>
      <div class="result">
        <div class="usage-comparison">
          <div class="usage-item">
            <h4>✅ 計算屬性適用場景</h4>
            <div class="scenario">
              <p><strong>過濾列表 (依賴 filterText)：</strong></p>
              <div class="filtered-list">
                <div v-for="item in filteredItems" :key="item.id" class="list-item">
                  {{ item.name }}
                </div>
              </div>
              <div class="performance-info">
                過濾計算次數：{{ filterCallCount }}
              </div>
            </div>
          </div>

          <div class="usage-item">
            <h4>✅ 方法適用場景</h4>
            <div class="scenario">
              <p><strong>格式化時間 (每次都需要最新值)：</strong></p>
              <div class="current-time">
                {{ getCurrentTime() }}
              </div>
              <div class="random-actions">
                <button @click="generateRandomNumber" class="btn btn-small">
                  生成隨機數：{{ getRandomNumber() }}
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// ✅ 計算屬性 - 適用於依賴響應式數據的計算
const filteredItems = computed(() => {
  return items.value.filter(item =>
    item.name.includes(filterText.value)
  )
})

// ✅ 方法 - 適用於每次都需要執行的操作
const getCurrentTime = () => {
  return new Date().toLocaleTimeString()
}

const getRandomNumber = () => {
  return Math.floor(Math.random() * 100)
}</code></pre>
      </div>
    </div>

    <!-- 效能比較 -->
    <div class="demo-section">
      <h3>3. 效能測試</h3>
      <div class="controls">
        <button @click="runPerformanceTest" class="btn btn-warning">
          執行效能測試
        </button>
        <button @click="clearResults" class="btn btn-secondary">
          清除結果
        </button>
      </div>
      <div class="result">
        <div v-if="performanceResults" class="performance-results">
          <h4>測試結果：</h4>
          <div class="test-result">
            <span>計算屬性執行時間：</span>
            <span class="time-value">{{ performanceResults.computed }}ms</span>
          </div>
          <div class="test-result">
            <span>方法執行時間：</span>
            <span class="time-value">{{ performanceResults.method }}ms</span>
          </div>
          <div class="test-result conclusion">
            <span>結論：</span>
            <span>{{ performanceResults.conclusion }}</span>
          </div>
        </div>
        <div v-else class="no-results">
          點擊「執行效能測試」查看結果
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 效能測試範例
const runPerformanceTest = () => {
  const iterations = 1000

  // 重置計數器
  const originalComputedCount = computedCallCount.value
  const originalMethodCount = methodCallCount.value

  // 測試計算屬性 (相同依賴，會使用快取)
  const computedStart = performance.now()
  for (let i = 0; i &lt; iterations; i++) {
    reversedMessageComputed.value // 多次訪問，但只計算一次
  }
  const computedTime = performance.now() - computedStart
  const computedExecutions = computedCallCount.value - originalComputedCount

  // 測試方法 (每次都重新執行)
  const methodStart = performance.now()
  for (let i = 0; i &lt; iterations; i++) {
    reversedMessageMethod() // 每次都執行
  }
  const methodTime = performance.now() - methodStart
  const methodExecutions = methodCallCount.value - originalMethodCount
}</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue'

// 快取機制比較
const message = ref('Hello Vue')
const computedCallCount = ref(0)
const methodCallCount = ref(0)
const forceUpdateKey = ref(0)
const methodResult = ref('')

const reversedMessageComputed = computed(() => {
  return message.value.split('').reverse().join('')
})

// 監聽計算屬性的變化來追蹤計算次數
watch(reversedMessageComputed, () => {
  computedCallCount.value++
}, { immediate: true })

const reversedMessageMethod = () => {
  methodCallCount.value++
  return message.value.split('').reverse().join('')
}

const callMethod = () => {
  methodResult.value = reversedMessageMethod()
}

// 初始化方法結果
callMethod()

// 使用時機範例
const listSize = ref(10)
const filterText = ref('')
const filterCallCount = ref(0)
const items = ref([])

// 生成初始數據
const generateItems = () => {
  const names = ['蘋果', '香蕉', '橘子', '葡萄', '草莓', '西瓜', '芒果', '鳳梨', '櫻桃', '藍莓']
  items.value = Array.from({ length: listSize.value }, (_, index) => ({
    id: index,
    name: names[index % names.length] + (index > 9 ? index : '')
  }))
}

// 初始化數據
generateItems()

const filteredItems = computed(() => {
  return items.value.filter(item =>
    item.name.includes(filterText.value)
  )
})

// 效能測試
const performanceResults = ref(null)

// 方法
const forceUpdate = () => {
  forceUpdateKey.value++
}

const addRandomItem = () => {
  const names = ['蘋果', '香蕉', '橘子', '葡萄', '草莓']
  const randomName = names[Math.floor(Math.random() * names.length)]
  items.value.push({
    id: items.value.length,
    name: randomName + Date.now()
  })
}

const getCurrentTime = () => {
  return new Date().toLocaleTimeString()
}

const getRandomNumber = () => {
  return Math.floor(Math.random() * 100)
}

const generateRandomNumber = () => {
  // 這個方法用於觸發重新渲染，展示方法每次都會執行
}

const runPerformanceTest = () => {
  const iterations = 1000

  // 重置計數器
  const originalComputedCount = computedCallCount.value
  const originalMethodCount = methodCallCount.value

  // 測試計算屬性 (相同依賴，會使用快取)
  const computedStart = performance.now()
  for (let i = 0; i < iterations; i++) {
    reversedMessageComputed.value // 多次訪問，但只計算一次
  }
  const computedTime = performance.now() - computedStart
  const computedExecutions = computedCallCount.value - originalComputedCount

  // 測試方法 (每次都重新執行)
  const methodStart = performance.now()
  for (let i = 0; i < iterations; i++) {
    reversedMessageMethod() // 每次都執行
  }
  const methodTime = performance.now() - methodStart
  const methodExecutions = methodCallCount.value - originalMethodCount

  performanceResults.value = {
    computed: computedTime.toFixed(2),
    method: methodTime.toFixed(2),
    conclusion: `計算屬性實際執行了 ${computedExecutions} 次，方法執行了 ${methodExecutions} 次，展示了快取效果`
  }
}

const clearResults = () => {
  performanceResults.value = null
  computedCallCount.value = 0
  methodCallCount.value = 0
  filterCallCount.value = 0
}
</script>
