<template>
  <div class="list-rendering-demo">
    <h2>響應式數組操作</h2>
    <p class="route-info">📍 路徑：/ListSamples/ReactiveArrayDemo.vue</p>
    <p class="description">
      在 Vue 2 中，某些數組操作不會觸發響應式更新，但在 Vue 3 中已經修復
    </p>

    <div class="demo-section">
      <h3>Vue 3 中的數組操作 (都是響應式的) <span class="code-path">ReactiveArrayDemo.vue</span></h3>
      <div class="controls">
        <button @click="directIndexAssignment" class="btn btn-primary">
          直接索引賦值 (Vue 2 中有問題)
        </button>
        <button @click="modifyLength" class="btn btn-primary">
          修改 length 屬性 (Vue 2 中有問題)
        </button>
        <button @click="resetReactiveList" class="btn btn-secondary">重置</button>
      </div>

      <div class="result">
        <div class="reactive-list">
          <div v-for="(item, index) in reactiveList" :key="item.id" class="reactive-item">
            <span>索引 {{ index }}: {{ item.name }} - {{ item.value }}</span>
          </div>
        </div>
      </div>

      <div class="code-example">
        <pre v-pre><code>// Vue 3 中所有數組操作都是響應式的
const list = ref([...])

// 直接索引賦值 - Vue 3 中可以正常工作
list.value[0] = newValue

// 修改 length 屬性 - Vue 3 中可以正常工作
list.value.length = 2</code></pre>
      </div>

      <div class="info-box">
        <h4>💡 Vue 2 中需要使用的解決方案：</h4>
        <pre v-pre><code>// Vue 2 中的解決方案
// 1. 使用 Vue.set 或 this.$set
this.$set(this.items, index, newValue)

// 2. 使用數組的 splice 方法
this.items.splice(index, 1, newValue)

// 3. 替換整個數組
this.items = [...this.items]</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// 響應式測試列表
const reactiveList = ref([
  { id: 1, name: 'Item 1', value: 100 },
  { id: 2, name: 'Item 2', value: 200 },
  { id: 3, name: 'Item 3', value: 300 }
])

// 響應式測試方法
const directIndexAssignment = () => {
  reactiveList.value[0] = {
    id: Date.now(),
    name: '直接賦值項目',
    value: 999
  }
}

const modifyLength = () => {
  reactiveList.value.length = 2
}

const resetReactiveList = () => {
  reactiveList.value = [
    { id: 1, name: 'Item 1', value: 100 },
    { id: 2, name: 'Item 2', value: 200 },
    { id: 3, name: 'Item 3', value: 300 }
  ]
}
</script>

<style scoped>
/* 組件樣式已在全域 main.css 中定義 */
</style>
