<!-- components/ComputedPropertiesDemo.vue -->
<template>
  <div class="computed-properties-demo">
    <h2>Vue 計算屬性示範 (Computed Properties)</h2>
    <p class="route-info">📍 路徑：/ComputedPropertiesDemo.vue</p>
    <p class="description">
      學習計算屬性的基本用法：唯讀與可寫計算屬性
    </p>

    <div class="demo-navigation">
      <button v-for="demo in demos" :key="demo.id" @click="currentDemo = demo.id"
        :class="['nav-btn', { active: currentDemo === demo.id }]">
        {{ demo.title }}
      </button>
    </div>

    <div class="demo-content">
      <ReadonlyComputedDemo v-if="currentDemo === 'readonly'" />
      <WritableComputedDemo v-else-if="currentDemo === 'writable'" />
      <ComputedVsMethodsDemo v-else-if="currentDemo === 'comparison'" />
      <StudentGradePractice v-else-if="currentDemo === 'student-grade'" />
      <SelfChallengeDemo v-else-if="currentDemo === 'self-challenge'" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import ReadonlyComputedDemo from './ComputedSamples/ReadonlyComputedDemo.vue'
import WritableComputedDemo from './ComputedSamples/WritableComputedDemo.vue'
import ComputedVsMethodsDemo from './ComputedSamples/ComputedVsMethodsDemo.vue'
import StudentGradePractice from './ComputedSamples/StudentGradePractice.vue'
import SelfChallengeDemo from './ComputedSamples/SelfChallengeDemo.vue'
const currentDemo = ref('readonly')

const demos = [
  { id: 'readonly', title: '唯讀計算屬性' },
  { id: 'writable', title: '可寫計算屬性' },
  { id: 'comparison', title: '計算屬性 vs 方法' },
  { id: 'student-grade', title: '實際案例:學生成績' },
  { id: 'self-challenge', title: '自我試煉' }
]
</script>

<style scoped>
/* 組件樣式已在全域 main.css 中定義 */
</style>
