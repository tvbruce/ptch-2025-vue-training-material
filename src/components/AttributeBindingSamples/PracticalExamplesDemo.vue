<!-- components/AttributeBindingSamples/PracticalExamplesDemo.vue -->
<template>
  <div class="practical-examples-demo">
    <h2>實際應用範例</h2>
    <p class="route-info">📍 路徑：/AttributeBindingSamples/PracticalExamplesDemo.vue</p>

    <!-- 主題切換器 -->
    <div class="demo-section">
      <h3>1. 主題切換器</h3>
      <div class="controls">
        <select v-model="currentTheme" class="select-field">
          <option value="light">淺色主題</option>
          <option value="dark">深色主題</option>
          <option value="blue">藍色主題</option>
          <option value="green">綠色主題</option>
        </select>
        <label class="checkbox-label">
          <input type="checkbox" v-model="enableAnimations">
          啟用動畫
        </label>
      </div>
      <div class="result">
        <div :class="themeClasses" :style="themeStyles" class="theme-container">
          <h4>主題預覽</h4>
          <p>這是一個動態主題的範例</p>
          <button :class="buttonClasses" @click="showThemeInfo">
            查看主題資訊
          </button>
          <div v-if="showInfo" class="theme-info">
            <p>當前主題：{{ currentTheme }}</p>
            <p>動畫：{{ enableAnimations ? '啟用' : '禁用' }}</p>
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 主題系統
const themeClasses = computed(() => ({
  [`theme-${currentTheme.value}`]: true,
  'animations-enabled': enableAnimations.value
}))

const themeStyles = computed(() => {
  const themes = {
    light: { '--bg-color': '#ffffff', '--text-color': '#333333' },
    dark: { '--bg-color': '#2c3e50', '--text-color': '#ecf0f1' },
    blue: { '--bg-color': '#3498db', '--text-color': '#ffffff' },
    green: { '--bg-color': '#27ae60', '--text-color': '#ffffff' }
  }
  return themes[currentTheme.value]
})</code></pre>
      </div>
    </div>

    <!-- 表單驗證 -->
    <div class="demo-section">
      <h3>2. 動態表單驗證</h3>
      <div class="form-container">
        <div class="form-field">
          <label>用戶名：</label>
          <input v-model="form.username" :class="usernameFieldClasses" :style="fieldStyles" placeholder="至少3個字符"
            class="form-input">
          <span :class="iconClasses.username">{{ getValidationIcon('username') }}</span>
          <div v-if="validationMessages.username" class="validation-message">
            {{ validationMessages.username }}
          </div>
        </div>

        <div class="form-field">
          <label>電子郵件：</label>
          <input v-model="form.email" :class="emailFieldClasses" :style="fieldStyles" placeholder="請輸入有效的電子郵件"
            class="form-input">
          <span :class="iconClasses.email">{{ getValidationIcon('email') }}</span>
          <div v-if="validationMessages.email" class="validation-message">
            {{ validationMessages.email }}
          </div>
        </div>

        <div class="form-field">
          <label>密碼：</label>
          <input v-model="form.password" :class="passwordFieldClasses" :style="fieldStyles" type="password"
            placeholder="至少6個字符" class="form-input">
          <span :class="iconClasses.password">{{ getValidationIcon('password') }}</span>
          <div v-if="validationMessages.password" class="validation-message">
            {{ validationMessages.password }}
          </div>
        </div>

        <button :disabled="!isFormValid" :class="submitButtonClasses" :style="submitButtonStyles" @click="submitForm"
          class="submit-btn">
          {{ submitButtonText }}
        </button>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 表單驗證
const usernameFieldClasses = computed(() => ({
  'field-valid': form.username.length >= 3,
  'field-invalid': form.username.length > 0 && form.username.length < 3,
  'field-empty': form.username.length === 0
}))

const validationMessages = computed(() => ({
  username: form.username.length > 0 && form.username.length < 3
    ? '用戶名至少需要3個字符' : '',
  email: form.email.length > 0 && !emailRegex.test(form.email)
    ? '請輸入有效的電子郵件地址' : '',
  password: form.password.length > 0 && form.password.length < 6
    ? '密碼至少需要6個字符' : ''
}))</code></pre>
      </div>
    </div>

    <!-- 響應式卡片 -->
    <div class="demo-section">
      <h3>3. 響應式卡片佈局</h3>
      <div class="controls">
        <input v-model.number="cardCount" type="range" min="1" max="12" class="range-input">
        <label>卡片數量: {{ cardCount }}</label>

        <select v-model="cardLayout" class="select-field">
          <option value="grid">網格佈局</option>
          <option value="flex">彈性佈局</option>
          <option value="masonry">瀑布流佈局</option>
        </select>

        <input v-model.number="cardSize" type="range" min="150" max="300" class="range-input">
        <label>卡片尺寸: {{ cardSize }}px</label>
      </div>
      <div class="result">
        <div :style="containerStyles" :class="containerClasses" class="cards-container">
          <div v-for="card in cardCount" :key="card" :style="cardStyles" :class="cardClasses" class="card"
            @mouseenter="hoveredCard = card" @mouseleave="hoveredCard = null">
            <div class="card-header">
              <h4>卡片 {{ card }}</h4>
              <span :class="{ 'card-active': hoveredCard === card }">
                {{ hoveredCard === card ? '🔥' : '📄' }}
              </span>
            </div>
            <p>這是卡片 {{ card }} 的內容</p>
            <button :style="{
              backgroundColor: `hsl(${(card * 30) % 360}, 70%, 50%)`,
              color: 'white',
              border: 'none',
              padding: '8px 16px',
              borderRadius: '4px',
              cursor: 'pointer'
            }">
              操作
            </button>
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 響應式卡片
const containerStyles = computed(() => ({
  display: cardLayout.value === 'grid' ? 'grid' : 'flex',
  gridTemplateColumns: cardLayout.value === 'grid'
    ? `repeat(auto-fill, minmax(${cardSize.value}px, 1fr))` : 'none',
  flexWrap: cardLayout.value === 'flex' ? 'wrap' : 'nowrap',
  gap: '15px',
  padding: '20px'
}))

const cardStyles = computed(() => ({
  width: cardLayout.value === 'flex' ? `${cardSize.value}px` : 'auto',
  minHeight: cardLayout.value === 'masonry' ? `${cardSize.value + Math.random() * 100}px` : `${cardSize.value}px`,
  transition: 'all 0.3s ease'
}))</code></pre>
      </div>
    </div>

    <!-- 進度指示器 -->
    <div class="demo-section">
      <h3>4. 動態進度指示器</h3>
      <div class="controls">
        <button @click="startProgress" class="btn btn-primary">
          {{ isProgressing ? '停止' : '開始' }}進度
        </button>
        <button @click="resetProgress" class="btn btn-secondary">
          重置進度
        </button>
        <select v-model="progressType" class="select-field">
          <option value="linear">線性進度條</option>
          <option value="circular">圓形進度條</option>
          <option value="step">步驟進度條</option>
        </select>
      </div>
      <div class="result">
        <div class="progress-container">
          <!-- 線性進度條 -->
          <div v-if="progressType === 'linear'" class="linear-progress">
            <div class="progress-label">進度: {{ Math.round(progress) }}%</div>
            <div class="progress-bar">
              <div :style="linearProgressStyles" :class="progressClasses" class="progress-fill"></div>
            </div>
          </div>

          <!-- 圓形進度條 -->
          <div v-else-if="progressType === 'circular'" class="circular-progress">
            <svg width="120" height="120" class="progress-svg">
              <circle cx="60" cy="60" r="50" fill="none" stroke="#e0e0e0" stroke-width="8" />
              <circle cx="60" cy="60" r="50" fill="none" :stroke="progressColor" stroke-width="8"
                :stroke-dasharray="circumference" :stroke-dashoffset="circularOffset" :style="circularProgressStyles"
                class="progress-circle" />
            </svg>
            <div class="progress-text">{{ Math.round(progress) }}%</div>
          </div>

          <!-- 步驟進度條 -->
          <div v-else class="step-progress">
            <div v-for="step in 5" :key="step" :class="stepClasses(step)" :style="stepStyles(step)"
              class="progress-step">
              <div class="step-number">{{ step }}</div>
              <div class="step-label">步驟 {{ step }}</div>
            </div>
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 進度指示器
const linearProgressStyles = computed(() => ({
  width: progress.value + '%',
  backgroundColor: progressColor.value,
  transition: 'all 0.3s ease'
}))

const circularProgressStyles = computed(() => ({
  transition: 'stroke-dashoffset 0.3s ease',
  transform: 'rotate(-90deg)',
  transformOrigin: '50% 50%'
}))

const stepClasses = (step) => ({
  'step-completed': progress.value >= (step - 1) * 20,
  'step-active': progress.value >= (step - 1) * 20 && progress.value < step * 20,
  'step-pending': progress.value < (step - 1) * 20
})</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onUnmounted } from 'vue'

// 主題切換
const currentTheme = ref('light')
const enableAnimations = ref(true)
const showInfo = ref(false)

const themeClasses = computed(() => ({
  [`theme-${currentTheme.value}`]: true,
  'animations-enabled': enableAnimations.value
}))

const themeStyles = computed(() => {
  const themes = {
    light: {
      '--bg-color': '#ffffff',
      '--text-color': '#333333',
      '--border-color': '#dee2e6'
    },
    dark: {
      '--bg-color': '#2c3e50',
      '--text-color': '#ecf0f1',
      '--border-color': '#34495e'
    },
    blue: {
      '--bg-color': '#3498db',
      '--text-color': '#ffffff',
      '--border-color': '#2980b9'
    },
    green: {
      '--bg-color': '#27ae60',
      '--text-color': '#ffffff',
      '--border-color': '#229954'
    }
  }
  return themes[currentTheme.value]
})

const buttonClasses = computed(() => ({
  'theme-button': true,
  [`theme-${currentTheme.value}-button`]: true
}))

// 表單驗證
const form = ref({
  username: '',
  email: '',
  password: ''
})

const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/

const usernameFieldClasses = computed(() => ({
  'field-valid': form.value.username.length >= 3,
  'field-invalid': form.value.username.length > 0 && form.value.username.length < 3,
  'field-empty': form.value.username.length === 0
}))

const emailFieldClasses = computed(() => ({
  'field-valid': emailRegex.test(form.value.email),
  'field-invalid': form.value.email.length > 0 && !emailRegex.test(form.value.email),
  'field-empty': form.value.email.length === 0
}))

const passwordFieldClasses = computed(() => ({
  'field-valid': form.value.password.length >= 6,
  'field-invalid': form.value.password.length > 0 && form.value.password.length < 6,
  'field-empty': form.value.password.length === 0
}))

const validationMessages = computed(() => ({
  username: form.value.username.length > 0 && form.value.username.length < 3
    ? '用戶名至少需要3個字符' : '',
  email: form.value.email.length > 0 && !emailRegex.test(form.value.email)
    ? '請輸入有效的電子郵件地址' : '',
  password: form.value.password.length > 0 && form.value.password.length < 6
    ? '密碼至少需要6個字符' : ''
}))

const iconClasses = computed(() => ({
  username: {
    'validation-icon': true,
    'icon-valid': form.value.username.length >= 3,
    'icon-invalid': form.value.username.length > 0 && form.value.username.length < 3
  },
  email: {
    'validation-icon': true,
    'icon-valid': emailRegex.test(form.value.email),
    'icon-invalid': form.value.email.length > 0 && !emailRegex.test(form.value.email)
  },
  password: {
    'validation-icon': true,
    'icon-valid': form.value.password.length >= 6,
    'icon-invalid': form.value.password.length > 0 && form.value.password.length < 6
  }
}))

const isFormValid = computed(() => {
  return form.value.username.length >= 3 &&
    emailRegex.test(form.value.email) &&
    form.value.password.length >= 6
})

const submitButtonClasses = computed(() => ({
  'btn-valid': isFormValid.value,
  'btn-invalid': !isFormValid.value
}))

const submitButtonStyles = computed(() => ({
  backgroundColor: isFormValid.value ? '#27ae60' : '#95a5a6',
  cursor: isFormValid.value ? 'pointer' : 'not-allowed',
  transform: isFormValid.value ? 'none' : 'none'
}))

const submitButtonText = computed(() => {
  return isFormValid.value ? '提交表單' : '請完成表單填寫'
})

const fieldStyles = {
  transition: 'all 0.3s ease'
}

// 響應式卡片
const cardCount = ref(6)
const cardLayout = ref('grid')
const cardSize = ref(200)
const hoveredCard = ref(null)

const containerStyles = computed(() => ({
  display: cardLayout.value === 'grid' ? 'grid' : 'flex',
  gridTemplateColumns: cardLayout.value === 'grid'
    ? `repeat(auto-fill, minmax(${cardSize.value}px, 1fr))` : 'none',
  flexWrap: cardLayout.value === 'flex' ? 'wrap' : 'nowrap',
  gap: '15px',
  padding: '20px',
  backgroundColor: '#f8f9fa',
  borderRadius: '8px',
  minHeight: '200px'
}))

const containerClasses = computed(() => ({
  [`layout-${cardLayout.value}`]: true
}))

const cardStyles = computed(() => ({
  width: cardLayout.value === 'flex' ? `${cardSize.value}px` : 'auto',
  minHeight: `${cardSize.value}px`,
  transition: 'all 0.3s ease'
}))

const cardClasses = computed(() => ({
  'card-hover': true
}))

// 進度指示器
const progress = ref(0)
const isProgressing = ref(false)
const progressType = ref('linear')
let progressTimer = null

const progressColor = computed(() => {
  if (progress.value < 30) return '#e74c3c'
  if (progress.value < 70) return '#f39c12'
  return '#27ae60'
})

const progressClasses = computed(() => ({
  'progress-low': progress.value < 30,
  'progress-medium': progress.value >= 30 && progress.value < 70,
  'progress-high': progress.value >= 70
}))

const linearProgressStyles = computed(() => ({
  width: progress.value + '%',
  backgroundColor: progressColor.value,
  transition: 'all 0.3s ease'
}))

const circumference = 2 * Math.PI * 50
const circularOffset = computed(() => {
  return circumference - (progress.value / 100) * circumference
})

const circularProgressStyles = computed(() => ({
  transition: 'stroke-dashoffset 0.3s ease',
  transform: 'rotate(-90deg)',
  transformOrigin: '50% 50%'
}))

const stepClasses = (step) => computed(() => ({
  'step-completed': progress.value >= (step - 1) * 20,
  'step-active': progress.value >= (step - 1) * 20 && progress.value < step * 20,
  'step-pending': progress.value < (step - 1) * 20
}))

const stepStyles = (step) => computed(() => ({
  borderColor: progress.value >= (step - 1) * 20 ? progressColor.value : '#dee2e6',
  backgroundColor: progress.value >= (step - 1) * 20 ? progressColor.value : 'white',
  color: progress.value >= (step - 1) * 20 ? 'white' : '#6c757d'
}))

// 方法
const showThemeInfo = () => {
  showInfo.value = !showInfo.value
}

const submitForm = () => {
  if (isFormValid.value) {
    alert('表單提交成功！')
  }
}

const getValidationIcon = (field) => {
  const fieldValue = form.value[field]

  if (field === 'username') {
    if (fieldValue.length === 0) return '⚪'
    return fieldValue.length >= 3 ? '✅' : '❌'
  }

  if (field === 'email') {
    if (fieldValue.length === 0) return '⚪'
    return emailRegex.test(fieldValue) ? '✅' : '❌'
  }

  if (field === 'password') {
    if (fieldValue.length === 0) return '⚪'
    return fieldValue.length >= 6 ? '✅' : '❌'
  }

  return '⚪'
}

const startProgress = () => {
  if (isProgressing.value) {
    clearInterval(progressTimer)
    isProgressing.value = false
  } else {
    isProgressing.value = true
    progressTimer = setInterval(() => {
      progress.value += 2
      if (progress.value >= 100) {
        progress.value = 100
        clearInterval(progressTimer)
        isProgressing.value = false
      }
    }, 100)
  }
}

const resetProgress = () => {
  clearInterval(progressTimer)
  progress.value = 0
  isProgressing.value = false
}

// 清理
onUnmounted(() => {
  if (progressTimer) {
    clearInterval(progressTimer)
  }
})
</script>

<style scoped>
/* 樣式已在 src/assets/main.css 中定義 */
</style>
