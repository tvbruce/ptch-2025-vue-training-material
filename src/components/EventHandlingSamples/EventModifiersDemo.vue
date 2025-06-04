<template>
  <div class="event-modifiers-demo">
    <h2>事件修飾符 (Event Modifiers)</h2>
    <p class="route-info">📍 路徑：/EventHandlingSamples/EventModifiersDemo.vue</p>

    <!-- .stop 修飾符 -->
    <div class="demo-section">
      <h3>1. .stop - 阻止事件冒泡</h3>
      <div class="result">
        <div class="bubble-demo">
          <div @click="logEvent('外層 div')" class="outer-box">
            外層容器 (點擊會觸發)
            <div @click="logEvent('內層 div')" class="inner-box normal">
              內層盒子 (正常冒泡)
            </div>
            <div @click.stop="logEvent('內層 div stop')" class="inner-box stop">
              內層盒子 (.stop 阻止冒泡)
            </div>
          </div>
        </div>
        <div class="event-log">
          <h5>事件日誌:</h5>
          <ul>
            <li v-for="(log, index) in eventLogs" :key="index">
              {{ log }}
            </li>
          </ul>
          <button @click="clearLogs" class="btn btn-small btn-secondary">清除日誌</button>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 阻止事件冒泡 -->
&lt;div @click="outerClick"&gt;
  &lt;div @click="innerClick"&gt;正常冒泡（會觸發外層）&lt;/div&gt;
  &lt;div @click.stop="innerClick"&gt;阻止冒泡（不會觸發外層）&lt;/div&gt;
&lt;/div&gt;</code></pre>
      </div>
    </div>

    <!-- .prevent 修飾符 -->
    <div class="demo-section">
      <h3>2. .prevent - 阻止預設行為</h3>
      <div class="result">
        <div class="prevent-examples">
          <form @submit="handleSubmit" class="demo-form">
            <h4>正常表單提交:</h4>
            <input v-model="formData.normalInput" placeholder="正常輸入" class="input-field">
            <button type="submit" class="btn btn-primary">提交 (會刷新頁面)</button>
          </form>

          <form @submit.prevent="handlePreventSubmit" class="demo-form">
            <h4>阻止預設行為:</h4>
            <input v-model="formData.preventInput" placeholder="阻止預設行為" class="input-field">
            <button type="submit" class="btn btn-success">提交 (.prevent 不會刷新)</button>
          </form>

          <div class="link-examples">
            <h4>連結範例:</h4>
            <a href="https://vuejs.org" target="_blank" class="demo-link">
              正常連結 (會跳轉)
            </a>
            <a href="https://vuejs.org" @click.prevent="handleLinkClick" class="demo-link">
              阻止跳轉 (.prevent)
            </a>
          </div>
        </div>
        <div class="action-result">
          <h5>操作結果:</h5>
          <p>{{ actionResult }}</p>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 阻止預設行為 -->
&lt;form @submit.prevent="handleSubmit"&gt;
  &lt;button type="submit"&gt;不會刷新頁面&lt;/button&gt;
&lt;/form&gt;

&lt;a href="#" @click.prevent="handleClick"&gt;不會跳轉&lt;/a&gt;</code></pre>
      </div>
    </div>

    <!-- .capture 修飾符 -->
    <div class="demo-section">
      <h3>3. .capture - 捕獲階段觸發</h3>
      <div class="result">
        <div class="capture-demo">
          <div @click.capture="logCapture('外層捕獲')" @click="logCapture('外層冒泡')" class="capture-outer">
            外層 (捕獲 + 冒泡)
            <div @click="logCapture('內層正常')" class="capture-inner">
              內層 (正常)
            </div>
          </div>
        </div>
        <div class="capture-log">
          <h5>捕獲事件日誌:</h5>
          <ul>
            <li v-for="(log, index) in captureLogs" :key="index">
              {{ log }}
            </li>
          </ul>
          <button @click="clearCaptureLogs" class="btn btn-small btn-secondary">清除日誌</button>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 在捕獲階段觸發事件處理器 -->
&lt;div @click.capture="captureHandler" @click="bubbleHandler"&gt;
  &lt;div @click="innerHandler"&gt;內層&lt;/div&gt;
&lt;/div&gt;

<!-- 執行順序：captureHandler → innerHandler → bubbleHandler --></code></pre>
      </div>
    </div>

    <!-- .self 修飾符 -->
    <div class="demo-section">
      <h3>4. .self - 只在點擊自身時觸發</h3>
      <div class="result">
        <div class="self-demo">
          <div @click="logSelf('外層正常')" class="self-outer normal">
            外層 (正常點擊)
            <div @click="logSelf('內層')" class="self-inner">內層</div>
          </div>
          <div @click.self="logSelf('外層 .self')" class="self-outer self-only">
            外層 (.self 只在點擊自身時觸發)
            <div @click="logSelf('內層')" class="self-inner">內層</div>
          </div>
        </div>
        <div class="self-log">
          <h5>Self 事件日誌:</h5>
          <ul>
            <li v-for="(log, index) in selfLogs" :key="index">
              {{ log }}
            </li>
          </ul>
          <button @click="clearSelfLogs" class="btn btn-small btn-secondary">清除日誌</button>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 只在 event.target 是當前元素自身時觸發 -->
&lt;div @click.self="onlyWhenClickSelf"&gt;
  &lt;div&gt;點擊這裡不會觸發父層事件&lt;/div&gt;
  點擊這裡會觸發事件
&lt;/div&gt;</code></pre>
      </div>
    </div>

    <!-- .once 修飾符 -->
    <div class="demo-section">
      <h3>5. .once - 只觸發一次</h3>
      <div class="result">
        <div class="once-examples">
          <button @click="normalClick" class="btn btn-primary">
            正常點擊 (次數: {{ normalClickCount }})
          </button>
          <button @click.once="onceClick" class="btn btn-warning">
            只能點擊一次 (次數: {{ onceClickCount }})
          </button>
          <button @click="resetOnce" class="btn btn-secondary">
            重置
          </button>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 事件只會觸發一次 -->
&lt;button @click.once="handleOnce"&gt;只能點擊一次&lt;/button&gt;</code></pre>
      </div>
    </div>

    <!-- .passive 修飾符 -->
    <div class="demo-section">
      <h3>6. .passive - 被動事件監聽</h3>
      <div class="result">
        <div class="passive-demo">
          <div @scroll="handleScroll" class="scroll-area normal">
            <h4>正常滾動監聽</h4>
            <div class="scroll-content">
              <p v-for="i in 20" :key="i">這是第 {{ i }} 行內容</p>
            </div>
          </div>
          <div @scroll.passive="handlePassiveScroll" class="scroll-area passive">
            <h4>被動滾動監聽 (.passive)</h4>
            <div class="scroll-content">
              <p v-for="i in 20" :key="i">這是第 {{ i }} 行內容</p>
            </div>
          </div>
        </div>
        <div class="scroll-info">
          <p><strong>正常滾動位置:</strong> {{ scrollPosition }}</p>
          <p><strong>被動滾動位置:</strong> {{ passiveScrollPosition }}</p>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 被動事件監聽，提高性能 -->
&lt;div @scroll.passive="handleScroll"&gt;
  <!-- 滾動內容 -->
&lt;/div&gt;

<!-- .passive 告訴瀏覽器這個監聽器不會調用 preventDefault() --></code></pre>
      </div>
    </div>

    <!-- 修飾符鏈式調用 -->
    <div class="demo-section">
      <h3>7. 修飾符鏈式調用</h3>
      <div class="result">
        <div class="chain-demo">
          <div @click="logChain('外層')" class="chain-outer">
            外層容器
            <form @submit.stop.prevent="handleChainSubmit" class="chain-form">
              <h4>鏈式修飾符範例:</h4>
              <input v-model="chainInput" placeholder="輸入內容" class="input-field">
              <button type="submit" class="btn btn-success">
                提交 (.stop.prevent)
              </button>
            </form>
            <div @click.self.once="logChain('Self Once')" class="chain-self">
              點擊空白處 (.self.once)
              <span>內層文字</span>
            </div>
          </div>
        </div>
        <div class="chain-result">
          <h5>鏈式操作結果:</h5>
          <p>{{ chainResult }}</p>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 修飾符可以鏈式調用 -->
&lt;form @submit.stop.prevent="handleSubmit"&gt;
  &lt;button type="submit"&gt;阻止冒泡和預設行為&lt;/button&gt;
&lt;/form&gt;

&lt;div @click.self.once="handleOnce"&gt;
  只在點擊自身時觸發，且只觸發一次
&lt;/div&gt;</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// 事件冒泡範例
const eventLogs = ref([])

const logEvent = (source) => {
  const timestamp = new Date().toLocaleTimeString()
  eventLogs.value.push(`${timestamp} - ${source}`)
}

const clearLogs = () => {
  eventLogs.value = []
}

// 阻止預設行為範例
const formData = ref({
  normalInput: '',
  preventInput: ''
})
const actionResult = ref('等待操作...')

const handleSubmit = () => {
  actionResult.value = '正常表單提交 (頁面可能會刷新)'
}

const handlePreventSubmit = () => {
  actionResult.value = `阻止預設提交，表單數據: ${formData.value.preventInput}`
}

const handleLinkClick = () => {
  actionResult.value = '阻止了連結跳轉行為'
}

// 事件捕獲範例
const captureLogs = ref([])

const logCapture = (phase) => {
  const timestamp = new Date().toLocaleTimeString()
  captureLogs.value.push(`${timestamp} - ${phase}`)
}

const clearCaptureLogs = () => {
  captureLogs.value = []
}

// .self 修飾符範例
const selfLogs = ref([])

const logSelf = (source) => {
  const timestamp = new Date().toLocaleTimeString()
  selfLogs.value.push(`${timestamp} - ${source}`)
}

const clearSelfLogs = () => {
  selfLogs.value = []
}

// .once 修飾符範例
const normalClickCount = ref(0)
const onceClickCount = ref(0)

const normalClick = () => {
  normalClickCount.value++
}

const onceClick = () => {
  onceClickCount.value++
}

const resetOnce = () => {
  normalClickCount.value = 0
  onceClickCount.value = 0
  // 注意：.once 修飾符重置需要重新渲染組件
}

// .passive 修飾符範例
const scrollPosition = ref(0)
const passiveScrollPosition = ref(0)

const handleScroll = (event) => {
  scrollPosition.value = event.target.scrollTop
}

const handlePassiveScroll = (event) => {
  passiveScrollPosition.value = event.target.scrollTop
}

// 修飾符鏈式調用範例
const chainInput = ref('')
const chainResult = ref('等待操作...')

const logChain = (source) => {
  chainResult.value = `觸發: ${source} - ${new Date().toLocaleTimeString()}`
}

const handleChainSubmit = () => {
  chainResult.value = `鏈式提交成功: ${chainInput.value} - 阻止了冒泡和預設行為`
}
</script>