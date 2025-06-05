<!-- components/WatcherSamples.vue -->
<template>
  <div class="watcher-samples">
    <h1>📡 偵聽器 (Watch & WatchEffect)</h1>
    <p class="description">數據變化的偵探，精確監控響應式狀態的變化</p>

    <!-- 範例導航 -->
    <div class="demo-navigation">
      <button v-for="demo in demos" :key="demo.id" @click="currentDemo = demo.id" class="nav-btn"
        :class="{ active: currentDemo === demo.id }">
        {{ demo.title }}
      </button>
    </div>

    <!-- 當前展示的範例 -->
    <component :is="currentComponent" />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import BasicWatchDemo from './WatcherSamples/BasicWatchDemo.vue'
import ComparisonDemo from './WatcherSamples/ComparisonDemo.vue'
import PracticalExamplesDemo from './WatcherSamples/PracticalExamplesDemo.vue'
import DataMonitorPractice from './WatcherSamples/DataMonitorPractice.vue'
import SelfChallengeDemo from './WatcherSamples/SelfChallengeDemo.vue'

const currentDemo = ref('basic')

const demos = [
  {
    id: 'basic',
    title: '基礎用法',
    component: BasicWatchDemo
  },
  {
    id: 'comparison',
    title: '對比選擇',
    component: ComparisonDemo
  },
  {
    id: 'practical',
    title: '實際應用',
    component: PracticalExamplesDemo
  },
  {
    id: 'data-monitor',
    title: '實際案例:資料監控',
    component: DataMonitorPractice
  },
  {
    id: 'self-challenge',
    title: '自我試煉',
    component: SelfChallengeDemo
  }
]

const currentComponent = computed(() => {
  const demo = demos.find(d => d.id === currentDemo.value)
  return demo ? demo.component : BasicWatchDemo
})
</script>

<style>
@import url('../assets/watcher.css');
</style>
