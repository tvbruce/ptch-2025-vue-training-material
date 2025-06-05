<!-- components/AttributeBindingDemo.vue -->
<template>
  <div class="attribute-binding-demo">
    <h2>Vue 屬性綁定示範 (v-bind / :class / :style)</h2>
    <p class="route-info">📍 路徑：/AttributeBindingDemo.vue</p>
    <p class="description">
      學習 Vue 的屬性綁定語法及其實際應用
    </p>

    <div class="demo-navigation">
      <button v-for="demo in demos" :key="demo.id" @click="currentDemo = demo.id"
        :class="['nav-btn', { active: currentDemo === demo.id }]">
        {{ demo.title }}
      </button>
    </div>

    <div class="demo-content">
      <BasicBindingDemo v-if="currentDemo === 'basic-binding'" />
      <ClassBindingDemo v-else-if="currentDemo === 'class-binding'" />
      <StyleBindingDemo v-else-if="currentDemo === 'style-binding'" />
      <DynamicAttributesDemo v-else-if="currentDemo === 'dynamic-attributes'" />
      <PracticalExamplesDemo v-else-if="currentDemo === 'practical-examples'" />
      <SelfChallengeDemo v-else-if="currentDemo === 'self-challenge'" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import BasicBindingDemo from './AttributeBindingSamples/BasicBindingDemo.vue'
import ClassBindingDemo from './AttributeBindingSamples/ClassBindingDemo.vue'
import StyleBindingDemo from './AttributeBindingSamples/StyleBindingDemo.vue'
import DynamicAttributesDemo from './AttributeBindingSamples/DynamicAttributesDemo.vue'
import PracticalExamplesDemo from './AttributeBindingSamples/PracticalExamplesDemo.vue'
import SelfChallengeDemo from './AttributeBindingSamples/SelfChallengeDemo.vue'

const currentDemo = ref('basic-binding')

const demos = [
  { id: 'basic-binding', title: '基礎屬性綁定' },
  { id: 'class-binding', title: 'Class 綁定' },
  { id: 'style-binding', title: 'Style 綁定' },
  { id: 'dynamic-attributes', title: '動態屬性' },
  { id: 'practical-examples', title: '實際應用' },
  { id: 'self-challenge', title: '🎯 自我試煉' }
]
</script>

<style scoped>
/* 組件樣式已在全域 main.css 中定義 */
</style>
