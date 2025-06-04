<template>
  <div class="conditional-rendering-demo">
    <h2>Vue 條件渲染示範 (v-if / v-else / v-show)</h2>
    <p class="route-info">📍 路徑：/ConditionalRenderingDemo.vue</p>
    <p class="description">
      學習 Vue 中不同的條件渲染指令及其適用場景
    </p>

    <div class="demo-navigation">
      <button v-for="demo in demos" :key="demo.id" @click="currentDemo = demo.id"
        :class="['nav-btn', { active: currentDemo === demo.id }]">
        {{ demo.title }}
      </button>
    </div>

    <div class="demo-content">
      <!-- 基礎條件渲染示範 -->
      <section v-if="currentDemo === 'basic'" class="demo-section">
        <h3>📚 基礎條件渲染
          <span class="code-path">components/ConditionalSamples/BasicConditionalDemo.vue</span>
        </h3>
        <BasicConditionalDemo />
      </section>

      <!-- v-if vs v-show 示範 -->
      <section v-else-if="currentDemo === 'performance'" class="demo-section">
        <h3>⚡ v-if vs v-show 性能比較
          <span class="code-path">components/ConditionalSamples/VIfVsVShowDemo.vue</span>
        </h3>
        <VIfVsVShowDemo />
      </section>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import BasicConditionalDemo from './ConditionalSamples/BasicConditionalDemo.vue'
import VIfVsVShowDemo from './ConditionalSamples/VIfVsVShowDemo.vue'

const currentDemo = ref('basic')

const demos = [
  { id: 'basic', title: '基礎條件渲染' },
  { id: 'performance', title: 'v-if vs v-show' }
]
</script>

<style scoped>
/* 組件樣式已在全域 main.css 中定義 */
</style>
