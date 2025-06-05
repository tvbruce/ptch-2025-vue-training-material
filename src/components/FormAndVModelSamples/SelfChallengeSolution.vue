<template>
  <div class="answering-area">
    <h2>🎯 參考答案 - 表單輸入與 v-model</h2>
    <p class="description">
      📝 <strong>任務：</strong>建立一個完整的使用者註冊系統，實作各種表單控制元件和驗證
    </p>

    <!-- 任務一：基本資料表單 -->
    <div class="task-section">
      <h3>👤 任務一：基本資料</h3>
      <div class="form-grid">
        <div class="form-group">
          <label>👤 使用者名稱：</label>
          <input v-model="formData.username" type="text" placeholder="請輸入使用者名稱" class="form-input"
            :class="{ 'error': errors.username }">
          <span v-if="errors.username" class="error-text">{{ errors.username }}</span>
        </div>

        <div class="form-group">
          <label>📧 電子郵件：</label>
          <input v-model="formData.email" type="email" placeholder="請輸入電子郵件" class="form-input"
            :class="{ 'error': errors.email }">
          <span v-if="errors.email" class="error-text">{{ errors.email }}</span>
        </div>

        <div class="form-group">
          <label>🔒 密碼：</label>
          <input v-model="formData.password" type="password" placeholder="請輸入密碼" class="form-input"
            :class="{ 'error': errors.password }">
          <span v-if="errors.password" class="error-text">{{ errors.password }}</span>
        </div>

        <div class="form-group">
          <label>🔒 確認密碼：</label>
          <input v-model="formData.confirmPassword" type="password" placeholder="請再次輸入密碼" class="form-input"
            :class="{ 'error': errors.confirmPassword }">
          <span v-if="errors.confirmPassword" class="error-text">{{ errors.confirmPassword }}</span>
        </div>
      </div>
    </div>

    <!-- 任務二：個人資訊 -->
    <div class="task-section">
      <h3>📝 任務二：個人資訊</h3>
      <div class="form-grid">
        <div class="form-group">
          <label>🎂 年齡：</label>
          <input v-model.number="formData.age" type="number" placeholder="請輸入年齡" class="form-input" min="0" max="120">
        </div>

        <div class="form-group">
          <label>👫 性別：</label>
          <div class="radio-group">
            <label class="radio-item">
              <input v-model="formData.gender" type="radio" value="male">
              <span>男性</span>
            </label>
            <label class="radio-item">
              <input v-model="formData.gender" type="radio" value="female">
              <span>女性</span>
            </label>
            <label class="radio-item">
              <input v-model="formData.gender" type="radio" value="other">
              <span>其他</span>
            </label>
          </div>
        </div>

        <div class="form-group">
          <label>🏠 居住城市：</label>
          <select v-model="formData.city" class="form-select">
            <option value="">請選擇城市</option>
            <option value="taipei">台北市</option>
            <option value="taichung">台中市</option>
            <option value="kaohsiung">高雄市</option>
            <option value="tainan">台南市</option>
            <option value="taoyuan">桃園市</option>
          </select>
        </div>

        <div class="form-group full-width">
          <label>💡 興趣愛好：</label>
          <div class="checkbox-group">
            <label class="checkbox-item">
              <input v-model="formData.hobbies" type="checkbox" value="reading">
              <span>閱讀</span>
            </label>
            <label class="checkbox-item">
              <input v-model="formData.hobbies" type="checkbox" value="music">
              <span>音樂</span>
            </label>
            <label class="checkbox-item">
              <input v-model="formData.hobbies" type="checkbox" value="sports">
              <span>運動</span>
            </label>
            <label class="checkbox-item">
              <input v-model="formData.hobbies" type="checkbox" value="travel">
              <span>旅遊</span>
            </label>
            <label class="checkbox-item">
              <input v-model="formData.hobbies" type="checkbox" value="cooking">
              <span>烹飪</span>
            </label>
            <label class="checkbox-item">
              <input v-model="formData.hobbies" type="checkbox" value="photography">
              <span>攝影</span>
            </label>
          </div>
        </div>

        <div class="form-group full-width">
          <label>📝 自我介紹：</label>
          <textarea v-model="formData.bio" placeholder="請簡單介紹一下自己..." class="form-textarea" rows="4"
            maxlength="500"></textarea>
          <div class="char-count" :class="{ 'warning': formData.bio.length > 400 }">
            {{ formData.bio.length }} / 500 字
          </div>
        </div>
      </div>
    </div>

    <!-- 任務三：設定選項 -->
    <div class="task-section">
      <h3>⚙️ 任務三：帳號設定</h3>
      <div class="form-grid">
        <div class="form-group">
          <label class="checkbox-item">
            <input v-model="formData.agreeTerms" type="checkbox">
            <span>我同意服務條款與隱私政策</span>
          </label>
        </div>

        <div class="form-group">
          <label class="checkbox-item">
            <input v-model="formData.newsletter" type="checkbox">
            <span>訂閱電子報</span>
          </label>
        </div>

        <div class="form-group">
          <label class="checkbox-item">
            <input v-model="formData.notifications" type="checkbox">
            <span>接收推播通知</span>
          </label>
        </div>
      </div>
    </div>

    <!-- 任務四：表單控制 -->
    <div class="task-section">
      <h3>🎛️ 任務四：表單操作</h3>
      <div class="form-actions">
        <button @click="validateForm" class="btn btn-primary">驗證表單</button>
        <button @click="submitForm" :disabled="!isFormValid" class="btn btn-success">提交註冊</button>
        <button @click="resetForm" class="btn btn-secondary">重置表單</button>
        <button @click="fillSampleData" class="btn btn-info">填入範例資料</button>
      </div>

      <div v-if="submitMessage" class="submit-message" :class="submitStatus">
        {{ submitMessage }}
      </div>
    </div>

    <!-- 任務五：資料預覽 -->
    <div class="task-section">
      <h3>👁️ 任務五：即時預覽</h3>
      <div class="preview-container">
        <h4>目前表單資料：</h4>
        <pre class="data-preview">{{ formDataPreview }}</pre>

        <h4>驗證狀態：</h4>
        <div class="validation-status">
          <div class="status-item" :class="{ 'valid': !errors.username, 'invalid': errors.username }">
            使用者名稱：{{ !errors.username ? '✅ 有效' : '❌ 無效' }}
          </div>
          <div class="status-item" :class="{ 'valid': !errors.email, 'invalid': errors.email }">
            電子郵件：{{ !errors.email ? '✅ 有效' : '❌ 無效' }}
          </div>
          <div class="status-item" :class="{ 'valid': !errors.password, 'invalid': errors.password }">
            密碼：{{ !errors.password ? '✅ 有效' : '❌ 無效' }}
          </div>
          <div class="status-item" :class="{ 'valid': !errors.confirmPassword, 'invalid': errors.confirmPassword }">
            確認密碼：{{ !errors.confirmPassword ? '✅ 有效' : '❌ 無效' }}
          </div>
        </div>
      </div>
    </div>

    <!-- 開發提示 -->
    <div class="hint-section">
      <h4>💡 開發提示</h4>
      <ul>
        <li>v-model 基本用法：綁定 input, textarea, select 等表單元素</li>
        <li>v-model 修飾符：.number（數字），.trim（去空格），.lazy（失焦時更新）</li>
        <li>表單驗證：實作即時驗證和提交前驗證</li>
        <li>checkbox 陣列：多選框可以綁定到陣列</li>
        <li>computed 計算屬性：用於表單狀態計算和資料格式化</li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue'

// 表單資料
const formData = ref({
  username: '',
  email: '',
  password: '',
  confirmPassword: '',
  age: null,
  gender: '',
  city: '',
  hobbies: [],
  bio: '',
  agreeTerms: false,
  newsletter: false,
  notifications: false
})

// 錯誤狀態
const errors = ref({
  username: '',
  email: '',
  password: '',
  confirmPassword: ''
})

// 提交狀態
const submitMessage = ref('')
const submitStatus = ref('')

// 使用者名稱驗證
const validateUsername = () => {
  const username = formData.value.username.trim()

  if (!username) {
    errors.value.username = '使用者名稱不能為空'
    return false
  }

  if (username.length < 3 || username.length > 20) {
    errors.value.username = '使用者名稱必須在3-20字元之間'
    return false
  }

  const usernameRegex = /^[a-zA-Z0-9_]+$/
  if (!usernameRegex.test(username)) {
    errors.value.username = '使用者名稱只能包含字母、數字和底線'
    return false
  }

  errors.value.username = ''
  return true
}

// 電子郵件驗證
const validateEmail = () => {
  const email = formData.value.email.trim()

  if (!email) {
    errors.value.email = '電子郵件不能為空'
    return false
  }

  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  if (!emailRegex.test(email)) {
    errors.value.email = '請輸入有效的電子郵件格式'
    return false
  }

  errors.value.email = ''
  return true
}

// 密碼驗證
const validatePassword = () => {
  const password = formData.value.password

  if (!password) {
    errors.value.password = '密碼不能為空'
    return false
  }

  if (password.length < 8) {
    errors.value.password = '密碼至少需要8個字元'
    return false
  }

  const hasUpperCase = /[A-Z]/.test(password)
  const hasLowerCase = /[a-z]/.test(password)
  const hasNumbers = /\d/.test(password)

  if (!hasUpperCase || !hasLowerCase || !hasNumbers) {
    errors.value.password = '密碼必須包含大寫字母、小寫字母和數字'
    return false
  }

  errors.value.password = ''
  return true
}

// 確認密碼驗證
const validateConfirmPassword = () => {
  const confirmPassword = formData.value.confirmPassword
  const password = formData.value.password

  if (!confirmPassword) {
    errors.value.confirmPassword = '請確認密碼'
    return false
  }

  if (confirmPassword !== password) {
    errors.value.confirmPassword = '密碼不一致'
    return false
  }

  errors.value.confirmPassword = ''
  return true
}

// 完整表單驗證
const validateForm = () => {
  const usernameValid = validateUsername()
  const emailValid = validateEmail()
  const passwordValid = validatePassword()
  const confirmPasswordValid = validateConfirmPassword()

  const isValid = usernameValid && emailValid && passwordValid && confirmPasswordValid

  if (isValid) {
    submitMessage.value = '✅ 表單驗證通過！'
    submitStatus.value = 'success'
  } else {
    submitMessage.value = '❌ 表單驗證失敗，請檢查錯誤項目'
    submitStatus.value = 'error'
  }

  // 自動清除訊息
  setTimeout(() => {
    submitMessage.value = ''
    submitStatus.value = ''
  }, 3000)

  return isValid
}

// 表單有效性檢查
const isFormValid = computed(() => {
  return !errors.value.username &&
    !errors.value.email &&
    !errors.value.password &&
    !errors.value.confirmPassword &&
    formData.value.username.trim() &&
    formData.value.email.trim() &&
    formData.value.password &&
    formData.value.confirmPassword &&
    formData.value.agreeTerms
})

// 表單資料預覽
const formDataPreview = computed(() => {
  return JSON.stringify({
    username: formData.value.username,
    email: formData.value.email,
    password: '***隱藏***',
    age: formData.value.age,
    gender: formData.value.gender,
    city: formData.value.city,
    hobbies: formData.value.hobbies,
    bio: formData.value.bio.substring(0, 50) + (formData.value.bio.length > 50 ? '...' : ''),
    agreeTerms: formData.value.agreeTerms,
    newsletter: formData.value.newsletter,
    notifications: formData.value.notifications
  }, null, 2)
})

// 提交表單
const submitForm = async () => {
  if (!validateForm()) {
    return
  }

  try {
    submitMessage.value = '提交中...'
    submitStatus.value = 'info'

    // 模擬 API 提交
    await new Promise(resolve => setTimeout(resolve, 2000))

    // 隨機決定成功或失敗（90% 成功率）
    if (Math.random() > 0.1) {
      submitMessage.value = '🎉 註冊成功！歡迎加入我們！'
      submitStatus.value = 'success'

      // 成功後重置表單
      setTimeout(() => {
        resetForm()
      }, 2000)
    } else {
      throw new Error('伺服器暫時無法處理請求')
    }

  } catch (error) {
    submitMessage.value = `❌ 註冊失敗：${error.message}`
    submitStatus.value = 'error'
  }
}

// 重置表單
const resetForm = () => {
  formData.value = {
    username: '',
    email: '',
    password: '',
    confirmPassword: '',
    age: null,
    gender: '',
    city: '',
    hobbies: [],
    bio: '',
    agreeTerms: false,
    newsletter: false,
    notifications: false
  }

  errors.value = {
    username: '',
    email: '',
    password: '',
    confirmPassword: ''
  }

  submitMessage.value = '表單已重置'
  submitStatus.value = 'success'

  setTimeout(() => {
    submitMessage.value = ''
    submitStatus.value = ''
  }, 2000)
}

// 填入範例資料
const fillSampleData = () => {
  formData.value = {
    username: 'john_doe',
    email: 'john.doe@example.com',
    password: 'Password123',
    confirmPassword: 'Password123',
    age: 25,
    gender: 'male',
    city: 'taipei',
    hobbies: ['reading', 'music', 'travel'],
    bio: '我是一名軟體工程師，熱愛程式設計和新技術學習。',
    agreeTerms: true,
    newsletter: true,
    notifications: false
  }

  // 觸發驗證
  validateForm()
}

// 監聽器：即時驗證
watch(() => formData.value.username, () => {
  if (formData.value.username.trim()) {
    validateUsername()
  } else {
    errors.value.username = ''
  }
})

watch(() => formData.value.email, () => {
  if (formData.value.email.trim()) {
    validateEmail()
  } else {
    errors.value.email = ''
  }
})

watch(() => formData.value.password, () => {
  if (formData.value.password) {
    validatePassword()
    // 如果確認密碼已經填寫，也要重新驗證
    if (formData.value.confirmPassword) {
      validateConfirmPassword()
    }
  } else {
    errors.value.password = ''
  }
})

watch(() => formData.value.confirmPassword, () => {
  if (formData.value.confirmPassword) {
    validateConfirmPassword()
  } else {
    errors.value.confirmPassword = ''
  }
})
</script>

<style scoped>
.answering-area {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

.task-section {
  background: #f8f9fa;
  padding: 2rem;
  border-radius: 8px;
  margin: 2rem 0;
  border-left: 4px solid #fd7e14;
}

.form-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1.5rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.form-group.full-width {
  grid-column: 1 / -1;
}

.form-group label {
  font-weight: bold;
  color: #495057;
}

.form-input,
.form-select,
.form-textarea {
  padding: 0.75rem;
  border: 2px solid #dee2e6;
  border-radius: 4px;
  font-size: 1rem;
  transition: border-color 0.3s ease;
}

.form-input:focus,
.form-select:focus,
.form-textarea:focus {
  outline: none;
  border-color: #fd7e14;
}

.form-input.error,
.form-select.error,
.form-textarea.error {
  border-color: #dc3545;
}

.error-text {
  color: #dc3545;
  font-size: 0.875rem;
  margin-top: 0.25rem;
}

.radio-group,
.checkbox-group {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}

.radio-item,
.checkbox-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  cursor: pointer;
  font-weight: normal;
}

.radio-item input,
.checkbox-item input {
  margin: 0;
}

.char-count {
  font-size: 0.875rem;
  color: #6c757d;
  text-align: right;
}

.char-count.warning {
  color: #fd7e14;
  font-weight: bold;
}

.form-actions {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}

.btn {
  padding: 0.75rem 1.5rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
  transition: all 0.3s ease;
}

.btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.btn-primary {
  background: #007bff;
  color: white;
}

.btn-primary:hover:not(:disabled) {
  background: #0056b3;
}

.btn-secondary {
  background: #6c757d;
  color: white;
}

.btn-secondary:hover:not(:disabled) {
  background: #545b62;
}

.btn-success {
  background: #28a745;
  color: white;
}

.btn-success:hover:not(:disabled) {
  background: #1e7e34;
}

.btn-info {
  background: #17a2b8;
  color: white;
}

.btn-info:hover:not(:disabled) {
  background: #117a8b;
}

.submit-message {
  margin-top: 1rem;
  padding: 1rem;
  border-radius: 4px;
  font-weight: bold;
  animation: fadeIn 0.3s ease-in;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }

  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.submit-message.success {
  background: #d4edda;
  color: #155724;
  border: 1px solid #c3e6cb;
}

.submit-message.error {
  background: #f8d7da;
  color: #721c24;
  border: 1px solid #f5c6cb;
}

.submit-message.info {
  background: #d1ecf1;
  color: #0c5460;
  border: 1px solid #bee5eb;
}

.preview-container {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.data-preview {
  background: #f8f9fa;
  padding: 1rem;
  border-radius: 4px;
  border: 1px solid #dee2e6;
  font-size: 0.875rem;
  overflow-x: auto;
  max-height: 300px;
  overflow-y: auto;
}

.validation-status {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
  margin-top: 1rem;
}

.status-item {
  padding: 0.5rem 1rem;
  border-radius: 4px;
  font-weight: bold;
  transition: all 0.3s ease;
}

.status-item.valid {
  background: #d4edda;
  color: #155724;
  border: 1px solid #c3e6cb;
}

.status-item.invalid {
  background: #f8d7da;
  color: #721c24;
  border: 1px solid #f5c6cb;
}

.hint-section {
  background: #fff3cd;
  padding: 1.5rem;
  border-radius: 8px;
  margin-top: 2rem;
  border-left: 4px solid #ffc107;
}

.hint-section ul {
  margin: 0.5rem 0;
  padding-left: 1.5rem;
}

.hint-section li {
  margin-bottom: 0.5rem;
}

@media (max-width: 768px) {
  .form-grid {
    grid-template-columns: 1fr;
  }

  .form-actions {
    flex-direction: column;
  }

  .validation-status {
    grid-template-columns: 1fr;
  }

  .radio-group,
  .checkbox-group {
    flex-direction: column;
    gap: 0.5rem;
  }
}
</style>
