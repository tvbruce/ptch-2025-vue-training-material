<!-- components/AttributeBindingSamples/ClassBindingDemo.vue -->
<template>
  <div class="class-binding-demo">
    <h2>Class 綁定 (:class)</h2>
    <p class="route-info">📍 路徑：/AttributeBindingSamples/ClassBindingDemo.vue</p>

    <!-- 物件語法 -->
    <div class="demo-section">
      <h3>1. 物件語法</h3>
      <div class="controls">
        <label class="checkbox-label">
          <input type="checkbox" v-model="isActive">
          啟用狀態 (active)
        </label>
        <label class="checkbox-label">
          <input type="checkbox" v-model="hasError">
          錯誤狀態 (error)
        </label>
        <label class="checkbox-label">
          <input type="checkbox" v-model="isLarge">
          大尺寸 (large)
        </label>
      </div>
      <div class="result">
        <div class="example-item">
          <h4>基本物件語法：</h4>
          <div :class="{ active: isActive, error: hasError, large: isLarge }" class="demo-box">
            我是測試元素
          </div>
          <div class="class-info">
            當前 class: {{ getCurrentClasses() }}
          </div>
        </div>

        <div class="example-item">
          <h4>使用計算屬性：</h4>
          <div :class="computedClasses" class="demo-box">
            我使用計算屬性
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 基本物件語法 -->
&lt;div :class="{ active: isActive, error: hasError, large: isLarge }"&gt;

<!-- 使用計算屬性 -->
const computedClasses = computed(() => ({
  active: isActive.value,
  error: hasError.value,
  large: isLarge.value,
  'has-content': true  // 可以使用引號包含連字符
}))</code></pre>
      </div>
    </div>

    <!-- 陣列語法 -->
    <div class="demo-section">
      <h3>2. 陣列語法</h3>
      <div class="controls">
        <select v-model="selectedTheme" class="select-field">
          <option value="">無主題</option>
          <option value="theme-blue">藍色主題</option>
          <option value="theme-green">綠色主題</option>
          <option value="theme-purple">紫色主題</option>
        </select>
        <select v-model="selectedSize" class="select-field">
          <option value="">預設大小</option>
          <option value="size-small">小尺寸</option>
          <option value="size-medium">中尺寸</option>
          <option value="size-large">大尺寸</option>
        </select>
        <label class="checkbox-label">
          <input type="checkbox" v-model="addBorder">
          添加邊框
        </label>
      </div>
      <div class="result">
        <div class="example-item">
          <h4>陣列語法：</h4>
          <div :class="[selectedTheme, selectedSize, addBorder ? 'bordered' : '']" class="demo-box">
            陣列語法範例
          </div>
        </div>

        <div class="example-item">
          <h4>陣列中使用物件：</h4>
          <div :class="[selectedTheme, { bordered: addBorder, [selectedSize]: selectedSize }]" class="demo-box">
            混合語法範例
          </div>
        </div>

        <div class="example-item">
          <h4>使用陣列計算屬性：</h4>
          <div :class="arrayClasses" class="demo-box">
            計算屬性陣列
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 陣列語法 -->
&lt;div :class="[selectedTheme, selectedSize, addBorder ? 'bordered' : '']"&gt;

<!-- 陣列中使用物件 -->
&lt;div :class="[selectedTheme, { bordered: addBorder }]"&gt;

<!-- 計算屬性陣列 -->
const arrayClasses = computed(() => {
  const classes = ['demo-box']
  if (selectedTheme.value) classes.push(selectedTheme.value)
  if (selectedSize.value) classes.push(selectedSize.value)
  if (addBorder.value) classes.push('bordered')
  return classes
})</code></pre>
      </div>
    </div>

    <!-- 動態切換 -->
    <div class="demo-section">
      <h3>3. 動態切換效果</h3>
      <div class="controls">
        <button @click="toggleAnimation" class="btn btn-primary">
          {{ isAnimating ? '停止動畫' : '開始動畫' }}
        </button>
        <button @click="cycleStates" class="btn btn-secondary">
          循環狀態
        </button>
        <button @click="randomState" class="btn btn-success">
          隨機狀態
        </button>
      </div>
      <div class="result">
        <div class="animation-demo">
          <div :class="animationClasses" class="animated-box">
            <div class="box-content">
              <h4>動態效果</h4>
              <p>狀態: {{ currentState }}</p>
            </div>
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 動態切換 class
const animationClasses = computed(() => ({
  'state-loading': currentState.value === 'loading',
  'state-success': currentState.value === 'success',
  'state-error': currentState.value === 'error',
  'state-warning': currentState.value === 'warning',
  'is-animating': isAnimating.value
}))

// 循環切換狀態
const cycleStates = () => {
  const states = ['loading', 'success', 'error', 'warning']
  const currentIndex = states.indexOf(currentState.value)
  const nextIndex = (currentIndex + 1) % states.length
  currentState.value = states[nextIndex]
}</code></pre>
      </div>
    </div>

    <!-- 條件式 Class -->
    <div class="demo-section">
      <h3>4. 條件式 Class 應用</h3>
      <div class="controls">
        <input v-model="username" placeholder="輸入用戶名" class="input-field">
        <input v-model="email" placeholder="輸入 Email" class="input-field">
        <input v-model="password" type="password" placeholder="輸入密碼" class="input-field">
      </div>
      <div class="result">
        <div class="form-validation">
          <div :class="usernameClasses" class="form-field">
            <label>用戶名：</label>
            <span>{{ username || '(未填寫)' }}</span>
            <span class="validation-icon">{{ getUsernameIcon() }}</span>
          </div>

          <div :class="emailClasses" class="form-field">
            <label>Email：</label>
            <span>{{ email || '(未填寫)' }}</span>
            <span class="validation-icon">{{ getEmailIcon() }}</span>
          </div>

          <div :class="passwordClasses" class="form-field">
            <label>密碼：</label>
            <span>{{ password ? '••••••••' : '(未填寫)' }}</span>
            <span class="validation-icon">{{ getPasswordIcon() }}</span>
          </div>

          <button :class="submitButtonClasses" class="submit-button" :disabled="!isFormValid">
            {{ isFormValid ? '提交表單' : '請完成表單' }}
          </button>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 表單驗證 class
const usernameClasses = computed(() => ({
  'field-valid': username.value.length >= 3,
  'field-invalid': username.value.length > 0 && username.value.length < 3,
  'field-empty': username.value.length === 0
}))

const emailClasses = computed(() => ({
  'field-valid': /\S+@\S+\.\S+/.test(email.value),
  'field-invalid': email.value.length > 0 && !/\S+@\S+\.\S+/.test(email.value),
  'field-empty': email.value.length === 0
}))

const submitButtonClasses = computed(() => ({
  'btn-enabled': isFormValid.value,
  'btn-disabled': !isFormValid.value
}))</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 物件語法
const isActive = ref(false)
const hasError = ref(false)
const isLarge = ref(false)

const computedClasses = computed(() => ({
  active: isActive.value,
  error: hasError.value,
  large: isLarge.value,
  'has-content': true
}))

// 陣列語法
const selectedTheme = ref('')
const selectedSize = ref('')
const addBorder = ref(false)

const arrayClasses = computed(() => {
  const classes = []
  if (selectedTheme.value) classes.push(selectedTheme.value)
  if (selectedSize.value) classes.push(selectedSize.value)
  if (addBorder.value) classes.push('bordered')
  return classes
})

// 動態切換
const isAnimating = ref(false)
const currentState = ref('loading')

const animationClasses = computed(() => ({
  'state-loading': currentState.value === 'loading',
  'state-success': currentState.value === 'success',
  'state-error': currentState.value === 'error',
  'state-warning': currentState.value === 'warning',
  'is-animating': isAnimating.value
}))

// 條件式 Class
const username = ref('')
const email = ref('')
const password = ref('')

const usernameClasses = computed(() => ({
  'field-valid': username.value.length >= 3,
  'field-invalid': username.value.length > 0 && username.value.length < 3,
  'field-empty': username.value.length === 0
}))

const emailClasses = computed(() => ({
  'field-valid': /\S+@\S+\.\S+/.test(email.value),
  'field-invalid': email.value.length > 0 && !/\S+@\S+\.\S+/.test(email.value),
  'field-empty': email.value.length === 0
}))

const passwordClasses = computed(() => ({
  'field-valid': password.value.length >= 6,
  'field-invalid': password.value.length > 0 && password.value.length < 6,
  'field-empty': password.value.length === 0
}))

const isFormValid = computed(() => {
  return username.value.length >= 3 &&
    /\S+@\S+\.\S+/.test(email.value) &&
    password.value.length >= 6
})

const submitButtonClasses = computed(() => ({
  'btn-enabled': isFormValid.value,
  'btn-disabled': !isFormValid.value
}))

// 方法
const getCurrentClasses = () => {
  const classes = ['demo-box']
  if (isActive.value) classes.push('active')
  if (hasError.value) classes.push('error')
  if (isLarge.value) classes.push('large')
  return classes.join(' ')
}

const toggleAnimation = () => {
  isAnimating.value = !isAnimating.value
}

const cycleStates = () => {
  const states = ['loading', 'success', 'error', 'warning']
  const currentIndex = states.indexOf(currentState.value)
  const nextIndex = (currentIndex + 1) % states.length
  currentState.value = states[nextIndex]
}

const randomState = () => {
  const states = ['loading', 'success', 'error', 'warning']
  const randomIndex = Math.floor(Math.random() * states.length)
  currentState.value = states[randomIndex]
}

const getUsernameIcon = () => {
  if (username.value.length === 0) return '⚪'
  return username.value.length >= 3 ? '✅' : '❌'
}

const getEmailIcon = () => {
  if (email.value.length === 0) return '⚪'
  return /\S+@\S+\.\S+/.test(email.value) ? '✅' : '❌'
}

const getPasswordIcon = () => {
  if (password.value.length === 0) return '⚪'
  return password.value.length >= 6 ? '✅' : '❌'
}
</script>

<style scoped>
/* 樣式已在 src/assets/main.css 中定義 */
</style>
