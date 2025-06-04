<!-- components/EventHandlingSamples/BasicEventDemo.vue -->
<template>
  <div class="basic-event-demo">
    <h2>基礎事件處理 (v-on)</h2>
    <p class="route-info">📍 路徑：/EventHandlingSamples/BasicEventDemo.vue</p>

    <!-- 基本 v-on 用法 -->
    <div class="demo-section">
      <h3>1. 基本 v-on 語法</h3>
      <div class="result">
        <div class="event-group">
          <h4>完整語法 v-on:</h4>
          <button v-on:click="incrementCounter" class="btn btn-primary">
            點擊次數: {{ clickCount }}
          </button>
          <button v-on:click="showAlert" class="btn btn-secondary">
            顯示警告
          </button>
        </div>

        <div class="event-group">
          <h4>簡寫語法 @:</h4>
          <button @click="incrementCounter" class="btn btn-success">
            點擊次數: {{ clickCount }}
          </button>
          <button @click="showMessage" class="btn btn-warning">
            顯示訊息
          </button>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 完整語法 -->
&lt;button v-on:click="incrementCounter"&gt;點擊&lt;/button&gt;
&lt;button v-on:click="showAlert"&gt;警告&lt;/button&gt;

<!-- 簡寫語法 (推薦) -->
&lt;button @click="incrementCounter"&gt;點擊&lt;/button&gt;
&lt;button @click="showMessage"&gt;訊息&lt;/button&gt;</code></pre>
      </div>
    </div>

    <!-- 內聯事件處理 -->
    <div class="demo-section">
      <h3>2. 內聯事件處理</h3>
      <div class="result">
        <div class="inline-examples">
          <button @click="counter++" class="btn btn-primary">
            簡單遞增: {{ counter }}
          </button>
          <button @click="message = '你好 Vue!'" class="btn btn-success">
            設定訊息
          </button>
          <button @click="items.push(`項目 ${items.length + 1}`)" class="btn btn-warning">
            新增項目
          </button>
          <button @click="showStatus = !showStatus" class="btn btn-secondary">
            切換狀態: {{ showStatus ? '顯示' : '隱藏' }}
          </button>
        </div>
        <div class="status-display">
          <p><strong>目前訊息:</strong> {{ message }}</p>
          <p v-if="showStatus" class="status-info">狀態已開啟！</p>
          <ul>
            <li v-for="item in items" :key="item">{{ item }}</li>
          </ul>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 內聯處理：直接在模板中寫 JavaScript -->
&lt;button @click="counter++"&gt;遞增&lt;/button&gt;
&lt;button @click="message = '你好 Vue!'"&gt;設定訊息&lt;/button&gt;
&lt;button @click="items.push(`項目 ${items.length + 1}`)"&gt;新增&lt;/button&gt;
&lt;button @click="showStatus = !showStatus"&gt;切換&lt;/button&gt;</code></pre>
      </div>
    </div>

    <!-- 帶參數的方法調用 -->
    <div class="demo-section">
      <h3>3. 帶參數的方法調用</h3>
      <div class="result">
        <div class="param-examples">
          <button @click="greet('Alice')" class="btn btn-primary">
            問候 Alice
          </button>
          <button @click="greet('Bob')" class="btn btn-primary">
            問候 Bob
          </button>
          <button @click="changeColor('red')" class="btn btn-danger">
            紅色
          </button>
          <button @click="changeColor('blue')" class="btn btn-primary">
            藍色
          </button>
          <button @click="changeColor('green')" class="btn btn-success">
            綠色
          </button>
        </div>
        <div class="param-output">
          <p><strong>問候訊息:</strong> {{ greetingMessage }}</p>
          <div class="color-box" :style="{ backgroundColor: currentColor }">
            目前顏色: {{ currentColor }}
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 傳遞參數給方法 -->
&lt;button @click="greet('Alice')"&gt;問候 Alice&lt;/button&gt;
&lt;button @click="changeColor('red')"&gt;設為紅色&lt;/button&gt;

// 方法定義
const greet = (name) => {
  greetingMessage.value = `你好，${name}！`
}

const changeColor = (color) => {
  currentColor.value = color
}</code></pre>
      </div>
    </div>

    <!-- 事件物件的使用 -->
    <div class="demo-section">
      <h3>4. 事件物件的使用</h3>
      <div class="result">
        <div class="event-object-examples">
          <button @click="handleClickEvent" class="btn btn-primary">
            獲取事件資訊
          </button>
          <input @input="handleInputEvent" v-model="inputValue" placeholder="輸入文字試試" class="input-field">
          <div @mousemove="handleMouseMove" class="mouse-area">
            滑鼠移動區域 ({{ mouseX }}, {{ mouseY }})
          </div>
        </div>
        <div class="event-info">
          <h5>事件資訊:</h5>
          <ul>
            <li><strong>事件類型:</strong> {{ eventInfo.type }}</li>
            <li><strong>目標元素:</strong> {{ eventInfo.target }}</li>
            <li><strong>時間戳記:</strong> {{ eventInfo.timestamp }}</li>
            <li><strong>輸入值:</strong> {{ inputValue }}</li>
          </ul>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 使用 $event 獲取事件物件 -->
&lt;button @click="handleClickEvent"&gt;獲取事件資訊&lt;/button&gt;
&lt;input @input="handleInputEvent" v-model="inputValue"&gt;
&lt;div @mousemove="handleMouseMove"&gt;滑鼠區域&lt;/div&gt;

// 方法中接收事件物件
const handleClickEvent = (event) => {
  eventInfo.value = {
    type: event.type,
    target: event.target.tagName,
    timestamp: new Date().toLocaleTimeString()
  }
}</code></pre>
      </div>
    </div>

    <!-- 同時使用事件物件和參數 -->
    <div class="demo-section">
      <h3>5. 同時使用事件物件和參數</h3>
      <div class="result">
        <div class="mixed-examples">
          <button @click="handleMixed('按鈕1', $event)" class="btn btn-primary">
            按鈕1
          </button>
          <button @click="handleMixed('按鈕2', $event)" class="btn btn-success">
            按鈕2
          </button>
          <button @click="handleMixed('按鈕3', $event)" class="btn btn-warning">
            按鈕3
          </button>
        </div>
        <div class="mixed-output">
          <p><strong>混合處理結果:</strong> {{ mixedResult }}</p>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 同時傳遞自定參數和事件物件 -->
&lt;button @click="handleMixed('按鈕1', $event)"&gt;按鈕1&lt;/button&gt;
&lt;button @click="handleMixed('按鈕2', $event)"&gt;按鈕2&lt;/button&gt;

// 方法接收多個參數
const handleMixed = (buttonName, event) => {
  const clickTime = new Date().toLocaleTimeString()
  mixedResult.value = `${buttonName} 在 ${clickTime} 被點擊 (元素: ${event.target.tagName})`
}</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// 基本計數器
const clickCount = ref(0)
const incrementCounter = () => {
  clickCount.value++
}

const showAlert = () => {
  alert('這是一個警告訊息！')
}

const showMessage = () => {
  alert('使用簡寫語法的訊息！')
}

// 內聯事件範例
const counter = ref(0)
const message = ref('初始訊息')
const showStatus = ref(false)
const items = ref(['項目 1'])

// 參數範例
const greetingMessage = ref('')
const currentColor = ref('lightgray')

const greet = (name) => {
  greetingMessage.value = `你好，${name}！`
}

const changeColor = (color) => {
  currentColor.value = color
}

// 事件物件範例
const inputValue = ref('')
const mouseX = ref(0)
const mouseY = ref(0)
const eventInfo = ref({
  type: '',
  target: '',
  timestamp: ''
})

const handleClickEvent = (event) => {
  eventInfo.value = {
    type: event.type,
    target: event.target.tagName,
    timestamp: new Date().toLocaleTimeString()
  }
}

const handleInputEvent = (event) => {
  eventInfo.value = {
    type: event.type,
    target: event.target.tagName,
    timestamp: new Date().toLocaleTimeString()
  }
}

const handleMouseMove = (event) => {
  mouseX.value = event.offsetX
  mouseY.value = event.offsetY
}

// 混合參數範例
const mixedResult = ref('')

const handleMixed = (buttonName, event) => {
  const clickTime = new Date().toLocaleTimeString()
  mixedResult.value = `${buttonName} 在 ${clickTime} 被點擊 (元素: ${event.target.tagName})`
}
</script>
