<!-- components/ComponentSamples.vue -->
<template>
  <div class="component-samples">
    <h1>Vue 組件化核心</h1>
    <p class="route-info">📍 路徑：/components/ComponentSamples.vue</p>
    <p class="description">
      學習 Vue 組件化的核心概念：Props 屬性傳遞、Emit 事件處理、Slot 插槽系統、動態組件與 Vue2/Vue3 開發方式對比。
    </p>

    <!-- 導航 -->
    <div class="demo-navigation">
      <button v-for="demo in demos" :key="demo.id" @click="currentDemo = demo.id"
        :class="['nav-btn', { active: currentDemo === demo.id }]">
        {{ demo.title }}
      </button>
    </div>

    <!-- 動態組件展示 -->
    <div class="demo-content">
      <component :is="currentComponent" />
    </div>

    <!-- 概念總結 -->
    <div class="demo-section">
      <h3>🎯 組件化核心概念總結</h3>
      <div class="concept-grid">
        <div class="concept-card">
          <h4>Props 屬性傳遞</h4>
          <ul>
            <li>父組件向子組件傳遞數據</li>
            <li>支持類型驗證和默認值</li>
            <li>單向數據流，子組件不能直接修改</li>
            <li>可傳遞基本類型、物件、陣列等</li>
          </ul>
        </div>
        <div class="concept-card">
          <h4>Emit 事件處理</h4>
          <ul>
            <li>子組件向父組件發送事件</li>
            <li>可以傳遞事件參數</li>
            <li>支持事件參數驗證</li>
            <li>實現組件間的雙向通信</li>
          </ul>
        </div>
        <div class="concept-card">
          <h4>Slot 插槽系統</h4>
          <ul>
            <li>默認插槽：基本內容插入</li>
            <li>具名插槽：多個插入點</li>
            <li>作用域插槽：訪問子組件數據</li>
            <li>動態插槽：動態插槽名稱</li>
          </ul>
        </div>
        <div class="concept-card">
          <h4>Vue2 vs Vue3 對比</h4>
          <ul>
            <li>Options API vs Composition API</li>
            <li>響應式數據聲明方式</li>
            <li>生命週期鉤子變化</li>
            <li>事件處理與方法定義</li>
          </ul>
        </div>
        <div class="concept-card">
          <h4>動態組件</h4>
          <ul>
            <li>根據條件動態切換組件</li>
            <li>Keep-Alive 保持組件狀態</li>
            <li>支持異步組件載入</li>
            <li>靈活的組件渲染方式</li>
          </ul>
        </div>
      </div>
    </div>

    <!-- 最佳實踐 -->
    <div class="demo-section">
      <h3>💡 組件設計最佳實踐</h3>
      <div class="best-practices">
        <div class="practice-item good">
          <h5>✅ 推薦做法</h5>
          <ul>
            <li>保持組件功能單一且專注</li>
            <li>使用 Props 進行父子通信</li>
            <li>通過 Emit 事件向上通信</li>
            <li>合理使用插槽提高靈活性</li>
            <li>組件命名要語義化</li>
            <li>適當使用 Keep-Alive 優化性能</li>
            <li>Vue3 優先使用 Composition API</li>
            <li>善用 ref 和 reactive 管理狀態</li>
          </ul>
        </div>
        <div class="practice-item caution">
          <h5>⚠️ 注意事項</h5>
          <ul>
            <li>不要直接修改 Props</li>
            <li>避免過度深層的組件嵌套</li>
            <li>謹慎使用作用域插槽，避免過度複雜</li>
            <li>動態組件要考慮性能影響</li>
            <li>事件命名要清晰明確</li>
            <li>組件要有適當的默認值和錯誤處理</li>
            <li>Vue2 項目升級 Vue3 需要逐步遷移</li>
            <li>注意 this 上下文在 Vue3 中的變化</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, shallowRef } from 'vue'
import PropsDemo from './ComponentSamples/PropsDemo.vue'
import EmitDemo from './ComponentSamples/EmitDemo.vue'
import SlotDemo from './ComponentSamples/SlotDemo.vue'
import DynamicComponentDemo from './ComponentSamples/DynamicComponentDemo.vue'
import ComponentPractice from './ComponentSamples/ComponentPractice.vue'
import SelfChallengeDemo from './ComponentSamples/SelfChallengeDemo.vue'
import SelfChallengeAnsweringArea from './ComponentSamples/SelfChallengeAnsweringArea.vue'
import SelfChallengeSolution from './ComponentSamples/SelfChallengeSolution.vue'
// 當前展示的組件
const currentDemo = ref('props')

// 可用的演示
const demos = shallowRef([
  { id: 'props', title: 'Props 屬性', component: PropsDemo },
  { id: 'emit', title: 'Emit 事件', component: EmitDemo },
  { id: 'slot', title: 'Slot 插槽', component: SlotDemo },
  { id: 'dynamic', title: '動態組件', component: DynamicComponentDemo },
  { id: 'component-practice', title: '實際案例:組件實戰', component: ComponentPractice },
  { id: 'self-challenge', title: '🎯 自我試煉題目', component: SelfChallengeDemo },
  { id: 'self-challenge-answering-area', title: '🎯 自我試煉實作區域', component: SelfChallengeAnsweringArea },
  { id: 'self-challenge-solution', title: '🎯 自我試煉解答', component: SelfChallengeSolution }
])

// 當前組件
const currentComponent = computed(() => {
  const demo = demos.value.find(d => d.id === currentDemo.value)
  return demo ? demo.component : PropsDemo
})
</script>
