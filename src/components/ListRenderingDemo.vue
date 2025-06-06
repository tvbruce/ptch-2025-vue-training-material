<template>
  <div class="list-rendering-demo">
    <h2>Vue 列表渲染示範 (v-for / key)</h2>
    <p class="route-info">📍 路徑：/ListRenderingDemo.vue</p>
    <p class="description">
      學習 v-for 指令的各種用法及最佳實踐
    </p>

    <div class="demo-navigation">
      <button v-for="demo in demos" :key="demo.id" @click="currentDemo = demo.id"
        :class="['nav-btn', { active: currentDemo === demo.id }]">
        {{ demo.title }}
      </button>
    </div>

    <div class="demo-content">
      <!-- 響應式陣列操作 -->
      <section v-if="currentDemo === 'reactive-array'" class="demo-section">
        <h3>🔄 響應式陣列操作
          <span class="code-path">components/ListSamples/ReactiveArrayDemo.vue</span>
        </h3>
        <ReactiveArrayDemo />
      </section>

      <!-- 物件迭代 -->
      <section v-else-if="currentDemo === 'object-iteration'" class="demo-section">
        <h3>🔄 物件迭代
          <span class="code-path">components/ListSamples/ObjectIterationDemo.vue</span>
        </h3>
        <ObjectIterationDemo />
      </section>

      <!-- 搜尋過濾 -->
      <section v-else-if="currentDemo === 'search-filter'" class="demo-section">
        <h3>🔍 搜尋與過濾
          <span class="code-path">components/ListSamples/SearchFilterDemo.vue</span>
        </h3>
        <SearchFilterDemo />
      </section>

      <!-- 分類切換 -->
      <section v-else-if="currentDemo === 'category-switch'" class="demo-section">
        <h3>📂 分類切換
          <span class="code-path">components/ListSamples/CategorySwitchDemo.vue</span>
        </h3>
        <CategorySwitchDemo />
      </section>

      <!-- Key 的重要性 -->
      <section v-else-if="currentDemo === 'key-importance'" class="demo-section">
        <h3>🔑 Key 的重要性
          <span class="code-path">components/ListSamples/KeyMissingDemo.vue</span>
        </h3>
        <KeyMissingDemo />
      </section>

      <!-- Index 作為 Key 的問題 -->
      <section v-else-if="currentDemo === 'index-key'" class="demo-section">
        <h3>⚠️ Index 作為 Key 的問題
          <span class="code-path">components/ListSamples/IndexKeyDemo.vue</span>
        </h3>
        <IndexKeyDemo />
      </section>

      <!-- 性能優化 -->
      <section v-else-if="currentDemo === 'performance'" class="demo-section">
        <h3>⚡ 性能優化
          <span class="code-path">components/ListSamples/PerformanceDemo.vue</span>
        </h3>
        <PerformanceDemo />
      </section>

      <!-- 購物車 -->
      <section v-else-if="currentDemo === 'shopping-cart'" class="demo-section">
        <h3>🛒 購物車
          <span class="code-path">components/ListSamples/ShoppingCartPractice.vue</span>
        </h3>
        <ShoppingCartPractice />
      </section>

      <!-- 自我試煉 -->
      <section v-else-if="currentDemo === 'self-challenge'" class="demo-section">
        <h3>🎯 自我試煉
          <span class="code-path">components/ListSamples/SelfChallengeDemo.vue</span>
        </h3>
        <SelfChallengeDemo />
      </section>

      <section v-else-if="currentDemo === 'self-challenge-answering-area'" class="demo-section">
        <h3>🎯 自我試煉實作區域
          <span class="code-path">components/ListSamples/SelfChallengeAnsweringArea.vue</span>
        </h3>
        <SelfChallengeAnsweringArea />
      </section>


      <!-- 自我試煉解答 -->
      <section v-else-if="currentDemo === 'self-challenge-solution'" class="demo-section">
        <h3>🎯 自我試煉解答
          <span class="code-path">components/ListSamples/SelfChallengeSolution.vue</span>
        </h3>
        <SelfChallengeSolution />
      </section>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import ReactiveArrayDemo from './ListSamples/ReactiveArrayDemo.vue'
import ObjectIterationDemo from './ListSamples/ObjectIterationDemo.vue'
import SearchFilterDemo from './ListSamples/SearchFilterDemo.vue'
import CategorySwitchDemo from './ListSamples/CategorySwitchDemo.vue'
import KeyMissingDemo from './ListSamples/KeyMissingDemo.vue'
import IndexKeyDemo from './ListSamples/IndexKeyDemo.vue'
import PerformanceDemo from './ListSamples/PerformanceDemo.vue'
import ShoppingCartPractice from './ListSamples/ShoppingCartPractice.vue'
import SelfChallengeDemo from './ListSamples/SelfChallengeDemo.vue'
import SelfChallengeAnsweringArea from './ListSamples/SelfChallengeAnsweringArea.vue'
import SelfChallengeSolution from './ListSamples/SelfChallengeSolution.vue'
const currentDemo = ref('reactive-array')

const demos = [
  { id: 'reactive-array', title: '響應式陣列' },
  { id: 'object-iteration', title: '物件迭代' },
  { id: 'search-filter', title: '搜尋過濾' },
  { id: 'category-switch', title: '分類切換' },
  { id: 'key-importance', title: 'Key 重要性' },
  { id: 'index-key', title: 'Index Key 問題' },
  { id: 'performance', title: '性能優化' },
  { id: 'shopping-cart', title: '實際案例:購物車' },
  { id: 'self-challenge', title: '🎯 自我試煉題目' },
  { id: 'self-challenge-answering-area', title: '🎯 自我試煉實作區域' },
  { id: 'self-challenge-solution', title: '🎯 自我試煉解答' }
]
</script>

<style scoped>
/* 組件樣式已在全域 main.css 中定義 */
</style>
