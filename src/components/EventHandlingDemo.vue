<!-- components/EventHandlingDemo.vue -->
<template>
  <div class="event-handling-demo">
    <h1>事件處理 (Event Handling)</h1>
    <p class="description">
      學習 Vue 3 的事件處理機制，包括基本事件綁定、事件修飾符、按鍵修飾符等。
      透過互動式範例理解如何響應使用者操作和處理各種 DOM 事件。
    </p>

    <!-- 範例導航 -->
    <div class="demo-navigation">
      <button v-for="demo in demos" :key="demo.id" @click="currentDemo = demo.id"
        :class="['nav-btn', { active: currentDemo === demo.id }]">
        <i :class="demo.icon"></i>
        {{ demo.title }}
      </button>
    </div>

    <!-- 當前範例組件 -->
    <component :is="currentComponent" :key="currentDemo" />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 導入範例組件
import BasicEventDemo from './EventHandlingSamples/BasicEventDemo.vue'
import EventModifiersDemo from './EventHandlingSamples/EventModifiersDemo.vue'
import KeyModifiersDemo from './EventHandlingSamples/KeyModifiersDemo.vue'
import InteractiveGamePractice from './EventHandlingSamples/InteractiveGamePractice.vue'

// 當前顯示的範例
const currentDemo = ref('basic')

// 所有範例配置
const demos = ref([
  {
    id: 'basic',
    title: '基礎事件處理',
    icon: '🎯',
    component: BasicEventDemo
  },
  {
    id: 'modifiers',
    title: '事件修飾符',
    icon: '⚙️',
    component: EventModifiersDemo
  },
  {
    id: 'keys',
    title: '按鍵修飾符',
    icon: '⌨️',
    component: KeyModifiersDemo
  },
  {
    id: 'interactive-game',
    title: '互動遊戲',
    icon: '🎮',
    component: InteractiveGamePractice
  }
])

// 組件映射
const componentMap = {
  'basic': BasicEventDemo,
  'modifiers': EventModifiersDemo,
  'keys': KeyModifiersDemo,
  'interactive-game': InteractiveGamePractice
}

// 當前組件
const currentComponent = computed(() => {
  return componentMap[currentDemo.value] || BasicEventDemo
})
</script>
