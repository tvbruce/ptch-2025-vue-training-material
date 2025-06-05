<!-- components/LifecycleDemo.vue -->
<template>
  <div class="lifecycle-demo">
    <h2>Vue 生命週期示範 (Lifecycle Hooks)</h2>
    <p class="route-info">📍 路徑：/LifecycleDemo.vue</p>
    <p class="description">
      學習組件生命週期的各個階段和使用時機
    </p>

    <div class="demo-navigation">
      <button v-for="demo in demos" :key="demo.id" @click="currentDemo = demo.id"
        :class="['nav-btn', { active: currentDemo === demo.id }]">
        {{ demo.title }}
      </button>
    </div>

    <div class="demo-content">
      <BasicLifecycleDemo v-if="currentDemo === 'basic'" />
      <LifecycleTimingDemo v-else-if="currentDemo === 'timing'" />
      <PracticalExamplesDemo v-else-if="currentDemo === 'practical'" />
      <TimerCounterPractice v-else-if="currentDemo === 'timer'" />
      <SelfChallengeDemo v-else-if="currentDemo === 'selfChallenge'" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import BasicLifecycleDemo from './LifecycleSamples/BasicLifecycleDemo.vue'
import LifecycleTimingDemo from './LifecycleSamples/LifecycleTimingDemo.vue'
import PracticalExamplesDemo from './LifecycleSamples/PracticalExamplesDemo.vue'
import TimerCounterPractice from './LifecycleSamples/TimerCounterPractice.vue'
import SelfChallengeDemo from './LifecycleSamples/SelfChallengeDemo.vue'
const currentDemo = ref('basic')

const demos = [
  { id: 'basic', title: '基本生命週期' },
  { id: 'timing', title: '執行時機' },
  { id: 'practical', title: '實際應用' },
  { id: 'timer', title: '計時器' },
  { id: 'selfChallenge', title: '自我挑戰' }
]
</script>

<style scoped>
/* 組件樣式已在全域 main.css 中定義 */
</style>
