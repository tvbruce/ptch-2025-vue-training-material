<!-- components/EventHandlingDemo.vue -->
<template>
  <div class="event-handling-demo">
    <h2>事件處理 (Event Handling)</h2>
    <p class="route-info">📍 路徑：/EventHandlingDemo.vue</p>
    <p class="description">
      學習 Vue 3 的事件處理機制，包括基本事件綁定、事件修飾符、按鍵修飾符等。
      透過互動式範例理解如何響應使用者操作和處理各種 DOM 事件。
    </p>

    <!-- 範例導航 -->
    <div class="demo-navigation">
      <button v-for="demo in demos" :key="demo.id" @click="currentDemo = demo.id"
        :class="['nav-btn', { active: currentDemo === demo.id }]">
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
import SelfChallengeDemo from './EventHandlingSamples/SelfChallengeDemo.vue'

// 當前顯示的範例
const currentDemo = ref('basic')

// 所有範例配置
const demos = ref([
  {
    id: 'basic',
    title: '基礎事件處理'
  },
  {
    id: 'modifiers',
    title: '事件修飾符'
  },
  {
    id: 'keys',
    title: '按鍵修飾符'
  },
  {
    id: 'interactive-game',
    title: '實際案例:互動遊戲'
  },
  {
    id: 'self-challenge',
    title: '自我試煉'
  }
])

// 組件映射
const componentMap = {
  'basic': BasicEventDemo,
  'modifiers': EventModifiersDemo,
  'keys': KeyModifiersDemo,
  'interactive-game': InteractiveGamePractice,
  'self-challenge': SelfChallengeDemo
}

// 當前組件
const currentComponent = computed(() => {
  return componentMap[currentDemo.value] || BasicEventDemo
})
</script>

<style scoped>
/* 組件樣式已在全域 main.css 中定義 */
</style>
