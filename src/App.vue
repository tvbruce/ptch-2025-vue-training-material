<template>
  <div id="app">
    <!-- 側邊欄 -->
    <aside class="sidebar" :class="{ 'sidebar-collapsed': isSidebarCollapsed }">
      <!-- 側邊欄標題 -->
      <div class="sidebar-header">
        <h2 v-if="!isSidebarCollapsed">Vue 3 教育訓練教材</h2>
        <button @click="toggleSidebar" class="sidebar-toggle">
          <i :class="isSidebarCollapsed ? 'icon-expand' : 'icon-collapse'"></i>
        </button>
      </div>

      <!-- 範例導航 -->
      <nav class="sidebar-nav">
        <ul class="nav-list">
          <li v-for="sample in samples" :key="sample.id" class="nav-item"
            :class="{ active: currentSample === sample.id }" @click="switchSample(sample.id)">
            <div class="nav-link">
              <i :class="sample.icon" class="nav-icon"></i>
              <span v-if="!isSidebarCollapsed" class="nav-text">{{ sample.title }}</span>
            </div>
          </li>
        </ul>
      </nav>
    </aside>

    <!-- 主要內容區域 -->
    <main class="main-content" :class="{ 'main-expanded': isSidebarCollapsed }">
      <!-- 頂部工具列 -->
      <header class="top-header">
        <div class="header-content">
          <h1 class="current-title">{{ getCurrentSample()?.title }}</h1>
          <div class="header-actions">
            <button @click="refreshSample" class="action-btn" title="重新載入">
              <i class="icon-refresh"></i>
            </button>
          </div>
        </div>
      </header>

      <!-- 範例內容 -->
      <div class="content-wrapper">
        <component :is="currentComponent" :key="currentSample" />
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 導入所有範例組件
import Vue2Vs3Comparison from './components/Vue2Vs3Comparison/Vue2Vs3ComparisonIndex.vue'
import ReactivityDemo from './components/ReactivityDemo.vue'
import AttributeBindingDemo from './components/AttributeBindingDemo.vue'
import ListRenderingDemo from './components/ListRenderingDemo.vue'
import ConditionalRenderingDemo from './components/ConditionalRenderingDemo.vue'
import ComputedPropertiesDemo from './components/ComputedPropertiesDemo.vue'
import LifecycleDemo from './components/LifecycleDemo.vue'
import EventHandlingDemo from './components/EventHandlingDemo.vue'
import WatcherSamples from './components/WatcherSamples.vue'
import ComponentSamples from './components/ComponentSamples.vue'
import FormAndVModelSamples from './components/FormAndVModelSamples.vue'

// 側邊欄狀態
const isSidebarCollapsed = ref(false)
const currentSample = ref('Reactivity')

// 範例組件映射
const componentMap = {
  'Vue2Vs3Comparison': Vue2Vs3Comparison,
  'Reactivity': ReactivityDemo,
  'AttributeBinding': AttributeBindingDemo,
  'ConditionalRendering': ConditionalRenderingDemo,
  'ListRendering': ListRenderingDemo,
  'ComputedProperties': ComputedPropertiesDemo,
  'Lifecycle': LifecycleDemo,
  'EventHandling': EventHandlingDemo,
  'Watcher': WatcherSamples,
  'Component': ComponentSamples,
  'FormAndVModel': FormAndVModelSamples
}

// 所有範例
const samples = ref([
  {
    id: 'Vue2Vs3Comparison',
    title: 'Vue 2 vs Vue 3 語法對比',
    icon: 'icon-vue2vs3'
  },
  {
    id: 'Reactivity',
    title: 'Reactivity 響應式',
    icon: 'icon-reactivity'
  },
  {
    id: 'AttributeBinding',
    title: 'Attribute 綁定',
    icon: 'icon-attribute'
  },
  {
    id: 'ConditionalRendering',
    title: 'v-if 條件渲染',
    icon: 'icon-branch'
  },

  {
    id: 'ListRendering',
    title: 'v-for 列表渲染',
    icon: 'icon-list'
  },
  {
    id: 'EventHandling',
    title: 'Event 事件處理',
    icon: 'icon-events'
  },
  {
    id: 'FormAndVModel',
    title: '表單輸入與 v-model',
    icon: 'icon-form'
  },
  {
    id: 'ComputedProperties',
    title: 'Computed 計算屬性',
    icon: 'icon-calculator'
  },
  {
    id: 'Watcher',
    title: 'Watcher 觀察者',
    icon: 'icon-watcher'
  },
  {
    id: 'Lifecycle',
    title: 'Lifecycle 生命週期',
    icon: 'icon-lifecycle'
  },
  {
    id: 'Component',
    title: 'Component 組件化',
    icon: 'icon-component'
  }
])

// 當前組件
const currentComponent = computed(() => {
  return componentMap[currentSample.value] || null
})

// 方法
const toggleSidebar = () => {
  isSidebarCollapsed.value = !isSidebarCollapsed.value
}

const switchSample = (sampleId) => {
  currentSample.value = sampleId
}

const getCurrentSample = () => {
  return samples.value.find(sample => sample.id === currentSample.value)
}

const refreshSample = () => {
  // 強制重新載入當前組件
  const temp = currentSample.value
  currentSample.value = ''
  setTimeout(() => {
    currentSample.value = temp
  }, 50)
}
</script>
