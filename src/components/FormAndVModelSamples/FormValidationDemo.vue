<template>
  <div class="form-validation-demo">
    <h2>表單驗證 (Form Validation)</h2>
    <p class="route-info">📍 路徑：/FormAndVModelSamples/FormValidationDemo.vue</p>

    <!-- 基礎欄位驗證 -->
    <div class="demo-section">
      <h3>1. 基礎欄位驗證</h3>
      <div class="demo-grid">
        <div class="demo-item">
          <label>必填欄位：</label>
          <input type="text" v-model="basicForm.name" placeholder="請輸入姓名" :class="getFieldClass('name')"
            @blur="validateField('name')">
          <div class="validation-info">
            <span v-if="basicErrors.name" class="field-invalid">
              ❌ {{ basicErrors.name }}
            </span>
            <span v-else-if="basicForm.name" class="field-valid">
              ✅ 姓名格式正確
            </span>
            <span v-else class="field-empty">
              📝 請輸入您的姓名
            </span>
          </div>
        </div>

        <div class="demo-item">
          <label>電子郵件：</label>
          <input type="email" v-model="basicForm.email" placeholder="請輸入電子郵件" :class="getFieldClass('email')"
            @blur="validateField('email')">
          <div class="validation-info">
            <span v-if="basicErrors.email" class="field-invalid">
              ❌ {{ basicErrors.email }}
            </span>
            <span v-else-if="basicForm.email && isValidEmail(basicForm.email)" class="field-valid">
              ✅ 電子郵件格式正確
            </span>
            <span v-else-if="basicForm.email" class="field-invalid">
              ❌ 請輸入有效的電子郵件格式
            </span>
            <span v-else class="field-empty">
              📧 請輸入您的電子郵件
            </span>
          </div>
        </div>
      </div>

      <div class="code-example">
        <pre v-pre><code>&lt;!-- 基礎欄位驗證 --&gt;
&lt;input
  type="text"
  v-model="basicForm.name"
  :class="getFieldClass('name')"
  @blur="validateField('name')"
&gt;

// 驗證方法
const validateField = (fieldName) => {
  const value = basicForm.value[fieldName]

  if (fieldName === 'name') {
    if (!value.trim()) {
      basicErrors.value.name = '姓名為必填欄位'
    } else if (value.length < 2) {
      basicErrors.value.name = '姓名至少需要2個字元'
    } else {
      delete basicErrors.value.name
    }
  }
}</code></pre>
      </div>
    </div>

    <!-- 即時驗證 -->
    <div class="demo-section">
      <h3>2. 即時驗證</h3>
      <div class="demo-grid">
        <div class="demo-item">
          <label>密碼強度檢查：</label>
          <input type="password" v-model="realtimeForm.password" placeholder="請輸入密碼"
            :class="getPasswordStrengthClass()">
          <div class="validation-info">
            <div class="password-strength">
              強度：<span :class="passwordStrength.class">{{ passwordStrength.text }}</span>
            </div>
            <ul class="password-requirements">
              <li :class="{ valid: passwordChecks.length }">
                {{ passwordChecks.length ? '✅' : '❌' }} 至少8個字元
              </li>
              <li :class="{ valid: passwordChecks.uppercase }">
                {{ passwordChecks.uppercase ? '✅' : '❌' }} 包含大寫字母
              </li>
              <li :class="{ valid: passwordChecks.lowercase }">
                {{ passwordChecks.lowercase ? '✅' : '❌' }} 包含小寫字母
              </li>
              <li :class="{ valid: passwordChecks.number }">
                {{ passwordChecks.number ? '✅' : '❌' }} 包含數字
              </li>
              <li :class="{ valid: passwordChecks.special }">
                {{ passwordChecks.special ? '✅' : '❌' }} 包含特殊字符
              </li>
            </ul>
          </div>
        </div>

        <div class="demo-item">
          <label>確認密碼：</label>
          <input type="password" v-model="realtimeForm.confirmPassword" placeholder="請再次輸入密碼"
            :class="getConfirmPasswordClass()">
          <div class="validation-info">
            <span v-if="realtimeForm.confirmPassword && passwordsMatch" class="field-valid">
              ✅ 密碼一致
            </span>
            <span v-else-if="realtimeForm.confirmPassword" class="field-invalid">
              ❌ 密碼不一致
            </span>
            <span v-else class="field-empty">
              🔐 請再次輸入密碼進行確認
            </span>
          </div>
        </div>
      </div>

      <div class="code-example">
        <pre v-pre><code>// 即時密碼強度檢查
const passwordChecks = computed(() => ({
  length: realtimeForm.value.password.length >= 8,
  uppercase: /[A-Z]/.test(realtimeForm.value.password),
  lowercase: /[a-z]/.test(realtimeForm.value.password),
  number: /\d/.test(realtimeForm.value.password),
  special: /[!@#$%^&*(),.?":{}|&lt;&gt;]/.test(realtimeForm.value.password)
}))

const passwordStrength = computed(() => {
  const checks = Object.values(passwordChecks.value)
  const score = checks.filter(Boolean).length

  if (score <= 2) return { text: '弱', class: 'weak' }
  if (score <= 3) return { text: '中等', class: 'medium' }
  if (score <= 4) return { text: '強', class: 'strong' }
  return { text: '非常強', class: 'very-strong' }
})</code></pre>
      </div>
    </div>

    <!-- 表單送出驗證 -->
    <div class="demo-section">
      <h3>3. 表單送出驗證</h3>
      <form @submit.prevent="handleSubmit" class="validation-form">
        <div class="demo-grid">
          <div class="demo-item">
            <label>使用者名稱：</label>
            <input type="text" v-model="submitForm.username" placeholder="請輸入使用者名稱"
              :class="getSubmitFieldClass('username')">
            <div class="validation-info" v-if="submitErrors.username">
              <span class="field-invalid">❌ {{ submitErrors.username }}</span>
            </div>
          </div>

          <div class="demo-item">
            <label>年齡：</label>
            <input type="number" v-model.number="submitForm.age" placeholder="請輸入年齡" min="18" max="100"
              :class="getSubmitFieldClass('age')">
            <div class="validation-info" v-if="submitErrors.age">
              <span class="field-invalid">❌ {{ submitErrors.age }}</span>
            </div>
          </div>

          <div class="demo-item">
            <label>手機號碼：</label>
            <input type="tel" v-model="submitForm.phone" placeholder="請輸入手機號碼 (09xxxxxxxx)"
              :class="getSubmitFieldClass('phone')">
            <div class="validation-info" v-if="submitErrors.phone">
              <span class="field-invalid">❌ {{ submitErrors.phone }}</span>
            </div>
          </div>

          <div class="demo-item">
            <label>
              <input type="checkbox" v-model="submitForm.agree">
              我同意服務條款
            </label>
            <div class="validation-info" v-if="submitErrors.agree">
              <span class="field-invalid">❌ {{ submitErrors.agree }}</span>
            </div>
          </div>
        </div>

        <div class="form-actions">
          <button type="submit" :disabled="!isFormValid" class="btn btn-primary">
            {{ isFormValid ? '送出表單' : '請完成必填欄位' }}
          </button>
          <button type="button" @click="resetForm" class="btn btn-secondary">
            重置表單
          </button>
        </div>
      </form>

      <div class="form-result" v-if="submitResult">
        <h4>表單送出結果：</h4>
        <pre>{{ JSON.stringify(submitResult, null, 2) }}</pre>
      </div>

      <div class="code-example">
        <pre v-pre><code>// 表單送出驗證
const handleSubmit = () => {
  // 清除之前的錯誤
  submitErrors.value = {}

  // 驗證所有欄位
  validateSubmitForm()

  // 如果有錯誤，停止送出
  if (Object.keys(submitErrors.value).length > 0) {
    return
  }

  // 模擬送出
  submitResult.value = { ...submitForm.value }
}

const validateSubmitForm = () => {
  if (!submitForm.value.username) {
    submitErrors.value.username = '使用者名稱為必填'
  } else if (!/^[a-zA-Z0-9_]{3,20}$/.test(submitForm.value.username)) {
    submitErrors.value.username = '使用者名稱只能包含字母、數字和底線，長度3-20字元'
  }

  if (!submitForm.value.agree) {
    submitErrors.value.agree = '請同意服務條款'
  }
}</code></pre>
      </div>
    </div>

    <!-- 自訂驗證規則 -->
    <div class="demo-section">
      <h3>4. 自訂驗證規則</h3>
      <div class="demo-grid">
        <div class="demo-item">
          <label>身分證字號：</label>
          <input type="text" v-model="customForm.idCard" placeholder="請輸入身分證字號 (A123456789)"
            :class="getCustomFieldClass('idCard')" @input="validateIdCard">
          <div class="validation-info">
            <span v-if="customErrors.idCard" class="field-invalid">
              ❌ {{ customErrors.idCard }}
            </span>
            <span v-else-if="customForm.idCard && isValidIdCard(customForm.idCard)" class="field-valid">
              ✅ 身分證字號格式正確
            </span>
            <span v-else-if="customForm.idCard" class="field-invalid">
              ❌ 身分證字號格式錯誤
            </span>
          </div>
        </div>

        <div class="demo-item">
          <label>信用卡號：</label>
          <input type="text" v-model="customForm.creditCard" placeholder="請輸入信用卡號 (1234 5678 9012 3456)"
            :class="getCustomFieldClass('creditCard')" @input="formatCreditCard" maxlength="19">
          <div class="validation-info">
            <span v-if="customErrors.creditCard" class="field-invalid">
              ❌ {{ customErrors.creditCard }}
            </span>
            <span v-else-if="customForm.creditCard && isValidCreditCard(customForm.creditCard)" class="field-valid">
              ✅ 信用卡號格式正確
            </span>
            <span v-else-if="customForm.creditCard" class="field-invalid">
              ❌ 信用卡號格式錯誤
            </span>
          </div>
        </div>
      </div>

      <div class="info-box">
        <h4>💡 自訂驗證提示</h4>
        <ul>
          <li>身分證字號：台灣身分證格式驗證 (英文字母 + 9位數字)</li>
          <li>信用卡號：使用 Luhn 演算法進行驗證</li>
          <li>可以根據業務需求自訂各種驗證規則</li>
        </ul>
      </div>

      <div class="code-example">
        <pre v-pre><code>// 身分證字號驗證
const isValidIdCard = (idCard) => {
  const pattern = /^[A-Z][12]\d{8}$/
  if (!pattern.test(idCard)) return false

  // 驗證檢查碼
  const letterValue = 'ABCDEFGHJKLMNPQRSTUVXYWZIO'.indexOf(idCard[0]) + 10
  const weights = [1, 9, 8, 7, 6, 5, 4, 3, 2, 1, 1]

  let sum = Math.floor(letterValue / 10) * weights[0] +
            (letterValue % 10) * weights[1]

  for (let i = 1; i < 10; i++) {
    sum += parseInt(idCard[i]) * weights[i + 1]
  }

  return sum % 10 === 0
}

// 信用卡號驗證 (Luhn算法)
const isValidCreditCard = (cardNumber) => {
  const cleaned = cardNumber.replace(/\s/g, '')
  if (!/^\d{13,19}$/.test(cleaned)) return false

  let sum = 0
  let shouldDouble = false

  for (let i = cleaned.length - 1; i >= 0; i--) {
    let digit = parseInt(cleaned[i])

    if (shouldDouble) {
      digit *= 2
      if (digit > 9) digit -= 9
    }

    sum += digit
    shouldDouble = !shouldDouble
  }

  return sum % 10 === 0
}</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, reactive } from 'vue'

// 基礎驗證表單
const basicForm = reactive({
  name: '',
  email: ''
})

const basicErrors = ref({})

// 即時驗證表單
const realtimeForm = reactive({
  password: '',
  confirmPassword: ''
})

// 表單送出驗證
const submitForm = reactive({
  username: '',
  age: null,
  phone: '',
  agree: false
})

const submitErrors = ref({})
const submitResult = ref(null)

// 自訂驗證表單
const customForm = reactive({
  idCard: '',
  creditCard: ''
})

const customErrors = ref({})

// 驗證方法
const validateField = (fieldName) => {
  const value = basicForm[fieldName]

  if (fieldName === 'name') {
    if (!value.trim()) {
      basicErrors.value.name = '姓名為必填欄位'
    } else if (value.length < 2) {
      basicErrors.value.name = '姓名至少需要2個字元'
    } else {
      delete basicErrors.value.name
    }
  }

  if (fieldName === 'email') {
    if (!value.trim()) {
      basicErrors.value.email = '電子郵件為必填欄位'
    } else if (!isValidEmail(value)) {
      basicErrors.value.email = '請輸入有效的電子郵件格式'
    } else {
      delete basicErrors.value.email
    }
  }
}

// 電子郵件驗證
const isValidEmail = (email) => {
  const pattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  return pattern.test(email)
}

// 密碼強度檢查
const passwordChecks = computed(() => ({
  length: realtimeForm.password.length >= 8,
  uppercase: /[A-Z]/.test(realtimeForm.password),
  lowercase: /[a-z]/.test(realtimeForm.password),
  number: /\d/.test(realtimeForm.password),
  special: /[!@#$%^&*(),.?":{}|<>]/.test(realtimeForm.password)
}))

const passwordStrength = computed(() => {
  const checks = Object.values(passwordChecks.value)
  const score = checks.filter(Boolean).length

  if (score <= 2) return { text: '弱', class: 'weak' }
  if (score <= 3) return { text: '中等', class: 'medium' }
  if (score <= 4) return { text: '強', class: 'strong' }
  return { text: '非常強', class: 'very-strong' }
})

const passwordsMatch = computed(() => {
  return realtimeForm.password && realtimeForm.confirmPassword &&
    realtimeForm.password === realtimeForm.confirmPassword
})

// 表單送出驗證
const validateSubmitForm = () => {
  submitErrors.value = {}

  if (!submitForm.username) {
    submitErrors.value.username = '使用者名稱為必填'
  } else if (!/^[a-zA-Z0-9_]{3,20}$/.test(submitForm.username)) {
    submitErrors.value.username = '使用者名稱只能包含字母、數字和底線，長度3-20字元'
  }

  if (!submitForm.age) {
    submitErrors.value.age = '年齡為必填'
  } else if (submitForm.age < 18 || submitForm.age > 100) {
    submitErrors.value.age = '年齡必須在18-100歲之間'
  }

  if (!submitForm.phone) {
    submitErrors.value.phone = '手機號碼為必填'
  } else if (!/^09\d{8}$/.test(submitForm.phone)) {
    submitErrors.value.phone = '請輸入有效的手機號碼格式 (09xxxxxxxx)'
  }

  if (!submitForm.agree) {
    submitErrors.value.agree = '請同意服務條款'
  }
}

const handleSubmit = () => {
  validateSubmitForm()

  if (Object.keys(submitErrors.value).length > 0) {
    return
  }

  // 模擬送出成功
  submitResult.value = { ...submitForm }
}

const resetForm = () => {
  submitForm.username = ''
  submitForm.age = null
  submitForm.phone = ''
  submitForm.agree = false
  submitErrors.value = {}
  submitResult.value = null
}

const isFormValid = computed(() => {
  return submitForm.username &&
    submitForm.age &&
    submitForm.phone &&
    submitForm.agree &&
    Object.keys(submitErrors.value).length === 0
})

// 身分證字號驗證
const validateIdCard = () => {
  if (!customForm.idCard) {
    delete customErrors.value.idCard
    return
  }

  if (!isValidIdCard(customForm.idCard)) {
    customErrors.value.idCard = '身分證字號格式錯誤'
  } else {
    delete customErrors.value.idCard
  }
}

const isValidIdCard = (idCard) => {
  const pattern = /^[A-Z][12]\d{8}$/
  if (!pattern.test(idCard)) return false

  // 驗證檢查碼
  const letterValue = 'ABCDEFGHJKLMNPQRSTUVXYWZIO'.indexOf(idCard[0]) + 10
  const weights = [1, 9, 8, 7, 6, 5, 4, 3, 2, 1, 1]

  let sum = Math.floor(letterValue / 10) * weights[0] +
    (letterValue % 10) * weights[1]

  for (let i = 1; i < 10; i++) {
    sum += parseInt(idCard[i]) * weights[i + 1]
  }

  return sum % 10 === 0
}

// 信用卡號格式化和驗證
const formatCreditCard = () => {
  let value = customForm.creditCard.replace(/\s/g, '')
  let formatted = value.replace(/(.{4})/g, '$1 ').trim()
  customForm.creditCard = formatted

  if (value.length >= 13) {
    if (!isValidCreditCard(customForm.creditCard)) {
      customErrors.value.creditCard = '信用卡號格式錯誤'
    } else {
      delete customErrors.value.creditCard
    }
  } else {
    delete customErrors.value.creditCard
  }
}

const isValidCreditCard = (cardNumber) => {
  const cleaned = cardNumber.replace(/\s/g, '')
  if (!/^\d{13,19}$/.test(cleaned)) return false

  let sum = 0
  let shouldDouble = false

  for (let i = cleaned.length - 1; i >= 0; i--) {
    let digit = parseInt(cleaned[i])

    if (shouldDouble) {
      digit *= 2
      if (digit > 9) digit -= 9
    }

    sum += digit
    shouldDouble = !shouldDouble
  }

  return sum % 10 === 0
}

// CSS 類別處理
const getFieldClass = (fieldName) => {
  if (basicErrors.value[fieldName]) return 'input-field error'
  if (basicForm[fieldName]) return 'input-field success'
  return 'input-field'
}

const getPasswordStrengthClass = () => {
  if (!realtimeForm.password) return 'input-field'
  const strength = passwordStrength.value.class
  return `input-field password-${strength}`
}

const getConfirmPasswordClass = () => {
  if (!realtimeForm.confirmPassword) return 'input-field'
  return passwordsMatch.value ? 'input-field success' : 'input-field error'
}

const getSubmitFieldClass = (fieldName) => {
  if (submitErrors.value[fieldName]) return 'input-field error'
  return 'input-field'
}

const getCustomFieldClass = (fieldName) => {
  if (customErrors.value[fieldName]) return 'input-field error'
  if (customForm[fieldName] &&
    ((fieldName === 'idCard' && isValidIdCard(customForm[fieldName])) ||
      (fieldName === 'creditCard' && isValidCreditCard(customForm[fieldName])))) {
    return 'input-field success'
  }
  return 'input-field'
}
</script>

<style scoped>
/* 樣式已在 src/assets/main.css 中定義 */
</style>
