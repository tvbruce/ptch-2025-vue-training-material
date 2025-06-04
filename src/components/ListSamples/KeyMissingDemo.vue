<template>
  <div class="list-rendering-demo">
    <h2>Key 的重要性</h2>
    <p class="route-info">📍 路徑：/ListSamples/KeyMissingDemo.vue</p>
    <p class="description">
      當列表項目順序改變時，沒有 key 會導致 Vue 錯誤復用 DOM 元素
    </p>

    <div class="demo-section">
      <h3>Key 對比測試 <span class="code-path">KeyMissingDemo.vue</span></h3>
      <div class="demo-container">
        <div class="demo-panel">
          <h4>❌ 錯誤示範 (沒有 key)</h4>
          <div class="controls">
            <button @click="shuffleLeftList" class="btn btn-warning">打亂順序</button>
            <button @click="resetLeftList" class="btn btn-secondary">重置</button>
          </div>

          <div class="result">
            <div class="user-list">
              <!-- eslint-disable-next-line vue/require-v-for-key -->
              <div v-for="user in filteredLeftUsers" class="user-item bad-example">
                <div class="user-info">
                  <span class="user-name">{{ user.name }}</span>
                  <span class="user-id">ID: {{ user.id }}</span>
                </div>
                <input :placeholder="`為 ${user.name} 輸入備註...`" class="user-input">
                <div class="user-color" :style="{ backgroundColor: user.color }"></div>
              </div>
            </div>
          </div>
        </div>

        <div class="demo-panel">
          <h4>✅ 正確示範 (有 key)</h4>
          <div class="controls">
            <button @click="shuffleRightList" class="btn btn-success">打亂順序</button>
            <button @click="resetRightList" class="btn btn-secondary">重置</button>
          </div>

          <div class="result">
            <div class="user-list">
              <div v-for="user in filteredRightUsers" :key="user.id" class="user-item good-example">
                <div class="user-info">
                  <span class="user-name">{{ user.name }}</span>
                  <span class="user-id">ID: {{ user.id }}</span>
                </div>
                <input :placeholder="`為 ${user.name} 輸入備註...`" class="user-input">
                <div class="user-color" :style="{ backgroundColor: user.color }"></div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="code-example">
        <pre v-pre><code><!-- 錯誤：沒有 key -->
&lt;div v-for="user in users"&gt;
  &lt;span&gt;{{ user.name }}&lt;/span&gt;
  &lt;input :placeholder="`為 ${user.name} 輸入備註...`"&gt;
&lt;/div&gt;

<!-- 正確：使用唯一的 key -->
&lt;div v-for="user in users" :key="user.id"&gt;
  &lt;span&gt;{{ user.name }}&lt;/span&gt;
  &lt;input :placeholder="`為 ${user.name} 輸入備註...`"&gt;
&lt;/div&gt;</code></pre>
      </div>

      <div class="explanation">
        <h4>🔍 測試步驟：</h4>
        <ol>
          <li>在左右兩邊的輸入框中分別輸入不同內容</li>
          <li>記住每個用戶對應的輸入內容</li>
          <li>分別點擊「打亂順序」按鈕</li>
          <li>觀察輸入框的內容是否跟著正確的用戶移動</li>
        </ol>
        <p><strong>預期結果：</strong>左側輸入內容會錯位，右側會正確跟隨</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 左側用戶列表 (沒有 key)
const leftUsers = ref([
  { id: 1, name: '張三', color: '#ff6b6b' },
  { id: 2, name: '李四', color: '#4ecdc4' },
  { id: 3, name: '王五', color: '#45b7d1' },
  { id: 4, name: '趙六', color: '#f9ca24' }
])

// 右側用戶列表 (有 key)
const rightUsers = ref([
  { id: 1, name: '張三', color: '#ff6b6b' },
  { id: 2, name: '李四', color: '#4ecdc4' },
  { id: 3, name: '王五', color: '#45b7d1' },
  { id: 4, name: '趙六', color: '#f9ca24' }
])

// 過濾有效的用戶
const filteredLeftUsers = computed(() => leftUsers.value.filter(user => user && user.name))
const filteredRightUsers = computed(() => rightUsers.value.filter(user => user && user.name))

// Fisher-Yates 洗牌算法
const shuffleArray = (array) => {
  const newArray = [...array]
  for (let i = newArray.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1))
      ;[newArray[i], newArray[j]] = [newArray[j], newArray[i]]
  }
  return newArray
}

const shuffleLeftList = () => {
  leftUsers.value = shuffleArray(leftUsers.value)
}

const shuffleRightList = () => {
  rightUsers.value = shuffleArray(rightUsers.value)
}

const resetLeftList = () => {
  leftUsers.value = [
    { id: 1, name: '張三', color: '#ff6b6b' },
    { id: 2, name: '李四', color: '#4ecdc4' },
    { id: 3, name: '王五', color: '#45b7d1' },
    { id: 4, name: '趙六', color: '#f9ca24' }
  ]
}

const resetRightList = () => {
  rightUsers.value = [
    { id: 1, name: '張三', color: '#ff6b6b' },
    { id: 2, name: '李四', color: '#4ecdc4' },
    { id: 3, name: '王五', color: '#45b7d1' },
    { id: 4, name: '趙六', color: '#f9ca24' }
  ]
}
</script>

<style scoped>
/* 組件樣式已在全域 main.css 中定義 */
</style>
