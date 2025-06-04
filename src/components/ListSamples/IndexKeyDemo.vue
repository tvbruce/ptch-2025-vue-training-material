<template>
  <div class="list-rendering-demo">
    <h2>Index 作為 Key 的問題</h2>
    <p class="route-info">📍 路徑：/ListSamples/IndexKeyDemo.vue</p>
    <p class="description">
      當列表項目會增刪時，使用 index 作為 key 會導致狀態錯亂
    </p>

    <div class="demo-section">
      <h3>Index Key 對比測試 <span class="code-path">IndexKeyDemo.vue</span></h3>
      <div class="demo-container">
        <div class="demo-panel">
          <h4>❌ 使用 index 作為 key</h4>
          <div class="controls">
            <button @click="addToTopLeft" class="btn btn-primary">頂部新增</button>
            <button @click="removeFirstLeft" class="btn btn-danger">刪除第一個</button>
            <button @click="resetLeftTasks" class="btn btn-secondary">重置</button>
          </div>

          <div class="result">
            <div class="task-list">
              <div v-for="(task, index) in leftTasks" :key="index" class="task-item bad-example">
                <span class="task-id">{{ task.name }}</span>
                <input type="checkbox" :id="`left-${index}`" class="task-checkbox">
                <label :for="`left-${index}`">完成狀態</label>
                <input :placeholder="`${task.name} 的備註`" class="task-input">
              </div>
            </div>
          </div>
        </div>

        <div class="demo-panel">
          <h4>✅ 使用唯一 ID 作為 key</h4>
          <div class="controls">
            <button @click="addToTopRight" class="btn btn-primary">頂部新增</button>
            <button @click="removeFirstRight" class="btn btn-danger">刪除第一個</button>
            <button @click="resetRightTasks" class="btn btn-secondary">重置</button>
          </div>

          <div class="result">
            <div class="task-list">
              <div v-for="task in rightTasks" :key="task.id" class="task-item good-example">
                <span class="task-id">{{ task.name }}</span>
                <input type="checkbox" :id="`right-${task.id}`" class="task-checkbox">
                <label :for="`right-${task.id}`">完成狀態</label>
                <input :placeholder="`${task.name} 的備註`" class="task-input">
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="code-example">
        <pre v-pre><code><!-- 錯誤：使用 index 作為 key -->
&lt;div v-for="(task, index) in tasks" :key="index"&gt;
  &lt;input type="checkbox" :id="`task-${index}`"&gt;
  &lt;input :placeholder="`${task.name} 的備註`"&gt;
&lt;/div&gt;

<!-- 正確：使用唯一 ID 作為 key -->
&lt;div v-for="task in tasks" :key="task.id"&gt;
  &lt;input type="checkbox" :id="`task-${task.id}`"&gt;
  &lt;input :placeholder="`${task.name} 的備註`"&gt;
&lt;/div&gt;</code></pre>
      </div>

      <div class="explanation">
        <h4>🔍 測試步驟：</h4>
        <ol>
          <li>勾選一些 checkbox 並在輸入框中填入內容</li>
          <li>點擊「頂部新增」添加新項目</li>
          <li>觀察原有項目的狀態是否保持正確</li>
          <li>點擊「刪除第一個」</li>
          <li>觀察剩餘項目的狀態</li>
        </ol>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// 左側任務列表 (index key)
const leftTasks = ref([
  { id: 1, name: '任務 A' },
  { id: 2, name: '任務 B' },
  { id: 3, name: '任務 C' }
])

// 右側任務列表 (id key)
const rightTasks = ref([
  { id: 1, name: '任務 A' },
  { id: 2, name: '任務 B' },
  { id: 3, name: '任務 C' }
])

let taskCounter = 4

const addToTopLeft = () => {
  leftTasks.value.unshift({ id: taskCounter++, name: `新任務 ${taskCounter - 1}` })
}

const addToTopRight = () => {
  rightTasks.value.unshift({ id: taskCounter++, name: `新任務 ${taskCounter - 1}` })
}

const removeFirstLeft = () => {
  leftTasks.value.shift()
}

const removeFirstRight = () => {
  rightTasks.value.shift()
}

const resetLeftTasks = () => {
  leftTasks.value = [
    { id: 1, name: '任務 A' },
    { id: 2, name: '任務 B' },
    { id: 3, name: '任務 C' }
  ]
  taskCounter = 4
}

const resetRightTasks = () => {
  rightTasks.value = [
    { id: 1, name: '任務 A' },
    { id: 2, name: '任務 B' },
    { id: 3, name: '任務 C' }
  ]
  taskCounter = 4
}
</script>

<style scoped>
/* 組件樣式已在全域 main.css 中定義 */
</style>
