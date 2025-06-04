<!-- components/AttributeBindingSamples/DynamicAttributesDemo.vue -->
<template>
  <div class="dynamic-attributes-demo">
    <h2>動態屬性綁定</h2>
    <p class="route-info">📍 路徑：/AttributeBindingSamples/DynamicAttributesDemo.vue</p>

    <!-- 動態屬性名 -->
    <div class="demo-section">
      <h3>1. 動態屬性名 v-bind:[attributeName]</h3>
      <div class="controls">
        <select v-model="selectedAttribute" class="select-field">
          <option value="title">title 屬性</option>
          <option value="placeholder">placeholder 屬性</option>
          <option value="data-info">data-info 屬性</option>
          <option value="aria-label">aria-label 屬性</option>
        </select>
        <input v-model="attributeValue" placeholder="輸入屬性值" class="input-field">
      </div>
      <div class="result">
        <div class="example-item">
          <h4>動態屬性綁定：</h4>
          <input v-bind:[selectedAttribute]="attributeValue" class="demo-input" value="測試輸入框">
          <div class="attribute-info">
            當前綁定：<code>{{ selectedAttribute }}="{{ attributeValue }}"</code>
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 動態屬性名語法 -->
&lt;input v-bind:[selectedAttribute]="attributeValue"&gt;

<!-- 簡寫 -->
&lt;input :[selectedAttribute]="attributeValue"&gt;

// JavaScript
const selectedAttribute = ref('title')
const attributeValue = ref('這是動態屬性值')</code></pre>
      </div>
    </div>

    <!-- 動態事件綁定 -->
    <div class="demo-section">
      <h3>2. 動態事件綁定 @[eventName]</h3>
      <div class="controls">
        <select v-model="selectedEvent" class="select-field">
          <option value="click">點擊事件 (click)</option>
          <option value="mouseover">滑鼠懸停 (mouseover)</option>
          <option value="focus">聚焦事件 (focus)</option>
          <option value="dblclick">雙擊事件 (dblclick)</option>
        </select>
        <button @click="resetEventLog" class="btn btn-secondary">清空日誌</button>
      </div>
      <div class="result">
        <div class="example-item">
          <h4>動態事件綁定：</h4>
          <button @[selectedEvent]="handleDynamicEvent" class="demo-button">
            觸發 {{ selectedEvent }} 事件
          </button>
          <input @[selectedEvent]="handleDynamicEvent" placeholder="或者在這裡觸發事件" class="demo-input">
          <div class="event-log">
            <h5>事件日誌：</h5>
            <div v-for="(log, index) in eventLogs" :key="index" class="log-item">
              {{ log }}
            </div>
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 動態事件綁定 -->
&lt;button @[selectedEvent]="handleDynamicEvent"&gt;

// JavaScript
const selectedEvent = ref('click')
const eventLogs = ref([])

const handleDynamicEvent = (event) => {
  const timestamp = new Date().toLocaleTimeString()
  eventLogs.value.unshift(`${timestamp}: ${selectedEvent.value} 事件被觸發`)
}</code></pre>
      </div>
    </div>

    <!-- 條件式屬性 -->
    <div class="demo-section">
      <h3>3. 條件式屬性綁定</h3>
      <div class="controls">
        <label class="checkbox-label">
          <input type="checkbox" v-model="showTooltip">
          顯示提示
        </label>
        <label class="checkbox-label">
          <input type="checkbox" v-model="isRequired">
          必填欄位
        </label>
        <label class="checkbox-label">
          <input type="checkbox" v-model="isDisabled">
          禁用狀態
        </label>
        <label class="checkbox-label">
          <input type="checkbox" v-model="addDataAttributes">
          添加 data 屬性
        </label>
      </div>
      <div class="result">
        <div class="example-item">
          <h4>條件式屬性：</h4>
          <input v-bind="conditionalAttributes" class="demo-input" placeholder="條件式屬性範例">
          <div class="attributes-display">
            <h5>當前屬性：</h5>
            <pre>{{ JSON.stringify(conditionalAttributes, null, 2) }}</pre>
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 條件式屬性物件
const conditionalAttributes = computed(() => {
  const attrs = {}

  if (showTooltip.value) {
    attrs.title = '這是一個提示訊息'
  }

  if (isRequired.value) {
    attrs.required = true
  }

  if (isDisabled.value) {
    attrs.disabled = true
  }

  if (addDataAttributes.value) {
    attrs['data-testid'] = 'dynamic-input'
    attrs['data-version'] = '1.0'
  }

  return attrs
})

&lt;input v-bind="conditionalAttributes"&gt;</code></pre>
      </div>
    </div>

    <!-- 動態組件屬性 -->
    <div class="demo-section">
      <h3>4. 動態組件屬性</h3>
      <div class="controls">
        <select v-model="componentType" class="select-field">
          <option value="button">按鈕組件</option>
          <option value="input">輸入框組件</option>
          <option value="link">連結組件</option>
        </select>
        <input v-model="dynamicText" placeholder="組件文字" class="input-field">
        <input v-model="dynamicUrl" placeholder="連結網址 (僅連結組件)" class="input-field">
      </div>
      <div class="result">
        <div class="example-item">
          <h4>動態組件：</h4>
          <component :is="componentType === 'button' ? 'button' : componentType === 'input' ? 'input' : 'a'"
            v-bind="dynamicComponentProps" class="dynamic-component">
            {{ componentType !== 'input' ? dynamicText : '' }}
          </component>

          <div class="component-info">
            <h5>當前組件屬性：</h5>
            <pre>{{ JSON.stringify(dynamicComponentProps, null, 2) }}</pre>
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 動態組件屬性
const dynamicComponentProps = computed(() => {
  const baseProps = {
    style: {
      padding: '10px 15px',
      borderRadius: '4px',
      border: '1px solid #ddd'
    }
  }

  switch (componentType.value) {
    case 'button':
      return {
        ...baseProps,
        type: 'button',
        onClick: () => alert('按鈕被點擊！')
      }
    case 'input':
      return {
        ...baseProps,
        type: 'text',
        placeholder: dynamicText.value || '請輸入...',
        value: ''
      }
    case 'link':
      return {
        ...baseProps,
        href: dynamicUrl.value || '#',
        target: '_blank',
        style: {
          ...baseProps.style,
          textDecoration: 'none',
          color: '#3498db'
        }
      }
    default:
      return baseProps
  }
})

&lt;component :is="componentTag" v-bind="dynamicComponentProps"&gt;</code></pre>
      </div>
    </div>

    <!-- 屬性修飾符 -->
    <div class="demo-section">
      <h3>5. 屬性修飾符與特殊情況</h3>
      <div class="controls">
        <input v-model="camelCaseAttr" placeholder="駝峰命名屬性值" class="input-field">
        <input v-model="kebabCaseAttr" placeholder="短橫線命名屬性值" class="input-field">
      </div>
      <div class="result">
        <div class="example-item">
          <h4>屬性命名轉換：</h4>
          <div :data-user-info="camelCaseAttr" :dataTestId="kebabCaseAttr" class="demo-element">
            檢查這個元素的屬性
          </div>

          <div class="naming-info">
            <h5>命名規則說明：</h5>
            <ul>
              <li><code>:data-user-info</code> → <code>data-user-info</code></li>
              <li><code>:dataTestId</code> → <code>data-test-id</code> (自動轉換)</li>
            </ul>
          </div>
        </div>

        <div class="example-item">
          <h4>特殊屬性處理：</h4>
          <input :value="inputValue" @input="inputValue = $event.target.value" class="demo-input" placeholder="受控輸入框">
          <div class="special-info">
            <p>輸入值：{{ inputValue }}</p>
            <p>這是受控組件的範例，使用 :value 和 @input</p>
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 屬性命名 -->
&lt;div :data-user-info="camelCaseAttr"&gt;  // kebab-case
&lt;div :dataTestId="kebabCaseAttr"&gt;      // 自動轉換為 data-test-id

<!-- 受控組件 -->
&lt;input
  :value="inputValue"
  @input="inputValue = $event.target.value"
&gt;

<!-- 等同於 v-model，但更明確 -->
&lt;input v-model="inputValue"&gt;</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 動態屬性名
const selectedAttribute = ref('title')
const attributeValue = ref('這是動態屬性值')

// 動態事件
const selectedEvent = ref('click')
const eventLogs = ref([])

// 條件式屬性
const showTooltip = ref(true)
const isRequired = ref(false)
const isDisabled = ref(false)
const addDataAttributes = ref(false)

const conditionalAttributes = computed(() => {
  const attrs = {}

  if (showTooltip.value) {
    attrs.title = '這是一個提示訊息'
  }

  if (isRequired.value) {
    attrs.required = true
  }

  if (isDisabled.value) {
    attrs.disabled = true
  }

  if (addDataAttributes.value) {
    attrs['data-testid'] = 'dynamic-input'
    attrs['data-version'] = '1.0'
  }

  return attrs
})

// 動態組件
const componentType = ref('button')
const dynamicText = ref('點我試試')
const dynamicUrl = ref('https://vuejs.org')

const dynamicComponentProps = computed(() => {
  const baseProps = {
    style: {
      padding: '10px 15px',
      borderRadius: '4px',
      border: '1px solid #ddd',
      backgroundColor: '#f8f9fa',
      cursor: 'pointer',
      transition: 'all 0.3s ease'
    }
  }

  switch (componentType.value) {
    case 'button':
      return {
        ...baseProps,
        type: 'button',
        onClick: () => alert('按鈕被點擊！')
      }
    case 'input':
      return {
        ...baseProps,
        type: 'text',
        placeholder: dynamicText.value || '請輸入...',
        style: {
          ...baseProps.style,
          cursor: 'text'
        }
      }
    case 'link':
      return {
        ...baseProps,
        href: dynamicUrl.value || '#',
        target: '_blank',
        style: {
          ...baseProps.style,
          textDecoration: 'none',
          color: '#3498db',
          display: 'inline-block'
        }
      }
    default:
      return baseProps
  }
})

// 屬性修飾符
const camelCaseAttr = ref('用戶資訊')
const kebabCaseAttr = ref('測試ID')
const inputValue = ref('')

// 方法
const handleDynamicEvent = (event) => {
  const timestamp = new Date().toLocaleTimeString()
  const eventType = selectedEvent.value
  const targetType = event.target.tagName.toLowerCase()

  eventLogs.value.unshift(
    `${timestamp}: ${eventType} 事件在 ${targetType} 元素上被觸發`
  )

  // 限制日誌數量
  if (eventLogs.value.length > 10) {
    eventLogs.value = eventLogs.value.slice(0, 10)
  }
}

const resetEventLog = () => {
  eventLogs.value = []
}
</script>

<style scoped>
/* 樣式已在 src/assets/main.css 中定義 */
</style>
