<!-- components/ReactivityDemo.vue -->
<template>
  <div class="reactivity-demo">
    <h2>Vue 響應式系統示範 (ref / reactive)</h2>
    <p class="route-info">📍 路徑：/ReactivityDemo.vue</p>
    <p class="description">
      學習 Vue 的響應式 API 及其使用場景
    </p>

    <div class="demo-navigation">
      <button v-for="demo in demos" :key="demo.id" @click="currentDemo = demo.id"
        :class="['nav-btn', { active: currentDemo === demo.id }]">
        {{ demo.title }}
      </button>
    </div>

    <div class="demo-content">
      <RefBasicsDemo v-if="currentDemo === 'ref-basics'" />
      <ReactiveBasicsDemo v-else-if="currentDemo === 'reactive-basics'" />
      <RefVsReactiveDemo v-else-if="currentDemo === 'comparison'" />
      <DeepReactivityDemo v-else-if="currentDemo === 'deep-reactivity'" />
      <WithoutReactivityDemo v-else-if="currentDemo === 'without-reactivity'" />
      <SelfChallengeDemo v-else-if="currentDemo === 'self-challenge'" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import RefBasicsDemo from './ReactivitySamples/RefBasicsDemo.vue'
import ReactiveBasicsDemo from './ReactivitySamples/ReactiveBasicsDemo.vue'
import RefVsReactiveDemo from './ReactivitySamples/RefVsReactiveDemo.vue'
import DeepReactivityDemo from './ReactivitySamples/DeepReactivityDemo.vue'
import WithoutReactivityDemo from './ReactivitySamples/WithoutReactivityDemo.vue'
import SelfChallengeDemo from './ReactivitySamples/SelfChallengeDemo.vue'

const currentDemo = ref('ref-basics')

const demos = [
  { id: 'ref-basics', title: 'ref 基礎用法' },
  { id: 'reactive-basics', title: 'reactive 基礎用法' },
  { id: 'comparison', title: 'ref vs reactive' },
  { id: 'deep-reactivity', title: '深層響應性' },
  { id: 'without-reactivity', title: '沒有響應式的對比' },
  { id: 'self-challenge', title: '自我試煉' }
]
</script>

<style scoped>
/* 組件樣式已在全域 main.css 中定義 */
</style>
