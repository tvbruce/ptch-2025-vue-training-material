<!-- components/ComponentSamples/DynamicComponentDemo.vue -->
<template>
    <div class="dynamic-component-demo">
        <h2>動態組件 (Dynamic Components)</h2>
        <p class="route-info">📍 路徑：/ComponentSamples/DynamicComponentDemo.vue</p>

        <!-- 基本動態組件 -->
        <div class="demo-section">
            <h3>1. 基本動態組件切換</h3>
            <div class="controls">
                <div class="tab-controls">
                    <button v-for="tab in tabs" :key="tab.name" @click="currentTab = tab.name"
                        :class="['tab-btn', { active: currentTab === tab.name }]">
                        {{ tab.label }}
                    </button>
                </div>
            </div>
            <div class="result">
                <component :is="currentComponent" :tab-data="getCurrentTabData()" />
            </div>
            <div class="code-example">
                <pre v-pre><code>// 基本動態組件用法
&lt;component :is="currentComponent" :tab-data="tabData" /&gt;

// 組件映射
const components = {
  'home': HomeTab,
  'profile': ProfileTab,
  'settings': SettingsTab
}

const currentComponent = computed(() => {
  return components[currentTab.value]
})</code></pre>
            </div>
        </div>

        <!-- Keep-Alive 保持狀態 -->
        <div class="demo-section">
            <h3>2. Keep-Alive 保持組件狀態</h3>
            <div class="controls">
                <div class="tab-controls">
                    <button v-for="tab in keepAliveTabs" :key="tab.name" @click="currentKeepAliveTab = tab.name"
                        :class="['tab-btn', { active: currentKeepAliveTab === tab.name }]">
                        {{ tab.label }}
                    </button>
                </div>
                <div class="info-box">
                    <p>使用 Keep-Alive 包裹的組件在切換時會保持狀態</p>
                </div>
            </div>
            <div class="result">
                <keep-alive>
                    <component :is="currentKeepAliveComponent" :key="currentKeepAliveTab" />
                </keep-alive>
            </div>
            <div class="code-example">
                <pre v-pre><code>// Keep-Alive 用法
&lt;keep-alive&gt;
  &lt;component :is="currentComponent" :key="currentTab" /&gt;
&lt;/keep-alive&gt;

// 或者指定包含/排除的組件
&lt;keep-alive :include="['ComponentA', 'ComponentB']"&gt;
  &lt;component :is="currentComponent" /&gt;
&lt;/keep-alive&gt;</code></pre>
            </div>
        </div>

        <!-- 條件動態組件 -->
        <div class="demo-section">
            <h3>3. 條件動態組件</h3>
            <div class="controls">
                <select v-model="selectedView" class="select-field">
                    <option value="list">列表視圖</option>
                    <option value="grid">網格視圖</option>
                    <option value="card">卡片視圖</option>
                </select>
                <label class="checkbox-label">
                    <input type="checkbox" v-model="showDetails">
                    顯示詳細信息
                </label>
            </div>
            <div class="result">
                <component :is="getViewComponent()" :items="sampleItems" :show-details="showDetails" />
            </div>
            <div class="code-example">
                <pre v-pre><code>// 條件動態組件
const getViewComponent = () => {
  const viewMap = {
    list: 'ListView',
    grid: 'GridView',
    card: 'CardView'
  }
  return viewMap[selectedView.value] || 'ListView'
}

&lt;component
  :is="getViewComponent()"
  :items="items"
  :show-details="showDetails"
/&gt;</code></pre>
            </div>
        </div>

        <!-- 動態組件與事件處理 -->
        <div class="demo-section">
            <h3>4. 動態組件事件處理</h3>
            <div class="controls">
                <select v-model="widgetType" class="select-field">
                    <option value="counter">計數器組件</option>
                    <option value="timer">計時器組件</option>
                    <option value="calculator">計算器組件</option>
                </select>
            </div>
            <div class="result">
                <component :is="getWidgetComponent()" @widget-action="handleWidgetAction"
                    @value-changed="handleValueChanged" />
                <div class="event-log">
                    <h5>事件記錄：</h5>
                    <ul>
                        <li v-for="(event, index) in eventHistory" :key="index">
                            {{ event }}
                        </li>
                        <li v-if="eventHistory.length === 0">尚無事件記錄</li>
                    </ul>
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code>// 動態組件事件處理
&lt;component
  :is="currentWidget"
  @widget-action="handleWidgetAction"
  @value-changed="handleValueChanged"
/&gt;

const handleWidgetAction = (action) => {
  console.log('組件動作:', action)
}

const handleValueChanged = (value) => {
  console.log('值變更:', value)
}</code></pre>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import HomeTab from './components/HomeTab.vue'
import ProfileTab from './components/ProfileTab.vue'
import SettingsTab from './components/SettingsTab.vue'
import CounterWidget from './components/CounterWidget.vue'
import TimerWidget from './components/TimerWidget.vue'
import CalculatorWidget from './components/CalculatorWidget.vue'
import ListView from './components/ListView.vue'
import GridView from './components/GridView.vue'
import CardView from './components/CardView.vue'

// 基本動態組件
const currentTab = ref('home')
const tabs = ref([
    { name: 'home', label: '首頁' },
    { name: 'profile', label: '個人資料' },
    { name: 'settings', label: '設定' }
])

const components = {
    'home': HomeTab,
    'profile': ProfileTab,
    'settings': SettingsTab
}

const currentComponent = computed(() => {
    return components[currentTab.value]
})

// Keep-Alive 動態組件
const currentKeepAliveTab = ref('counter')
const keepAliveTabs = ref([
    { name: 'counter', label: '計數器' },
    { name: 'timer', label: '計時器' },
    { name: 'calculator', label: '計算器' }
])

const keepAliveComponents = {
    'counter': CounterWidget,
    'timer': TimerWidget,
    'calculator': CalculatorWidget
}

const currentKeepAliveComponent = computed(() => {
    return keepAliveComponents[currentKeepAliveTab.value]
})

// 條件動態組件
const selectedView = ref('list')
const showDetails = ref(false)
const sampleItems = ref([
    { id: 1, name: '項目 1', description: '這是第一個項目的描述' },
    { id: 2, name: '項目 2', description: '這是第二個項目的描述' },
    { id: 3, name: '項目 3', description: '這是第三個項目的描述' },
    { id: 4, name: '項目 4', description: '這是第四個項目的描述' }
])

// 動態組件事件處理
const widgetType = ref('counter')
const eventHistory = ref([])

// 方法
const getCurrentTabData = () => {
    const tabData = {
        home: { message: '歡迎來到首頁!' },
        profile: { user: { name: '張三', email: 'zhang@example.com' } },
        settings: { theme: 'light', language: 'zh-TW' }
    }
    return tabData[currentTab.value] || {}
}

const getViewComponent = () => {
    const viewMap = {
        list: ListView,
        grid: GridView,
        card: CardView
    }
    return viewMap[selectedView.value] || ListView
}

const getWidgetComponent = () => {
    const widgetMap = {
        counter: CounterWidget,
        timer: TimerWidget,
        calculator: CalculatorWidget
    }
    return widgetMap[widgetType.value] || CounterWidget
}

const handleWidgetAction = (action) => {
    const timestamp = new Date().toLocaleTimeString()
    eventHistory.value.push(`[${timestamp}] 動作: ${action}`)
    if (eventHistory.value.length > 10) {
        eventHistory.value.shift()
    }
}

const handleValueChanged = (value) => {
    const timestamp = new Date().toLocaleTimeString()
    eventHistory.value.push(`[${timestamp}] 值變更: ${value}`)
    if (eventHistory.value.length > 10) {
        eventHistory.value.shift()
    }
}
</script>
