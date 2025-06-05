<template>
  <div class="self-challenge-solution">
    <h2>🎯 自我試煉解答 - 表單輸入與 v-model</h2>
    <p class="route-info">📍 路徑：/FormAndVModelSamples/SelfChallengeSolution.vue</p>

    <div class="form-container">
      <h3>📝 用戶資料表單</h3>

      <!-- 表單區域 -->
      <form @submit="submitForm" class="user-form">
        <!-- 基本資訊 -->
        <div class="form-section">
          <h4>基本資訊</h4>

          <div class="form-group">
            <label for="name">姓名 *</label>
            <input id="name" v-model.trim="formData.name" type="text" placeholder="請輸入姓名"
              :class="{ 'error': formData.name.trim().length > 0 && formData.name.trim().length < 2 }">
            <span v-if="formData.name.trim().length > 0 && formData.name.trim().length < 2" class="error-text">
              姓名至少需要2個字元
            </span>
          </div>

          <div class="form-group">
            <label for="email">Email *</label>
            <input id="email" v-model.trim="formData.email" type="email" placeholder="請輸入Email"
              :class="{ 'error': formData.email && !validateEmail(formData.email) }">
            <span v-if="formData.email && !validateEmail(formData.email)" class="error-text">
              請輸入有效的Email格式
            </span>
          </div>

          <div class="form-group">
            <label for="age">年齡 *</label>
            <input id="age" v-model.number="formData.age" type="number" min="1" max="120" @input="handleAgeInput"
              :class="{ 'error': formData.age < 18 || formData.age > 100 }">
            <span v-if="formData.age < 18 || formData.age > 100" class="error-text">
              年齡必須在18-100歲之間
            </span>
          </div>
        </div>

        <!-- 選擇項目 -->
        <div class="form-section">
          <h4>個人資訊</h4>

          <div class="form-group">
            <label>性別 *</label>
            <div class="radio-group">
              <label class="radio-label">
                <input type="radio" v-model="formData.gender" value="male">
                <span>男性</span>
              </label>
              <label class="radio-label">
                <input type="radio" v-model="formData.gender" value="female">
                <span>女性</span>
              </label>
              <label class="radio-label">
                <input type="radio" v-model="formData.gender" value="other">
                <span>其他</span>
              </label>
            </div>
          </div>

          <div class="form-group">
            <label for="country">國家</label>
            <select id="country" v-model="formData.country">
              <option value="">請選擇國家</option>
              <option value="taiwan">台灣</option>
              <option value="china">中國</option>
              <option value="japan">日本</option>
              <option value="korea">韓國</option>
              <option value="usa">美國</option>
            </select>
          </div>

          <div class="form-group">
            <label>興趣愛好 *</label>
            <div class="checkbox-group">
              <label class="checkbox-label">
                <input type="checkbox" v-model="formData.interests" value="reading">
                <span>閱讀</span>
              </label>
              <label class="checkbox-label">
                <input type="checkbox" v-model="formData.interests" value="music">
                <span>音樂</span>
              </label>
              <label class="checkbox-label">
                <input type="checkbox" v-model="formData.interests" value="sports">
                <span>運動</span>
              </label>
              <label class="checkbox-label">
                <input type="checkbox" v-model="formData.interests" value="travel">
                <span>旅遊</span>
              </label>
              <label class="checkbox-label">
                <input type="checkbox" v-model="formData.interests" value="cooking">
                <span>烹飪</span>
              </label>
            </div>
            <span v-if="formData.interests.length === 0" class="error-text">
              請至少選擇一項興趣
            </span>
          </div>

          <div class="form-group">
            <label>語言能力</label>
            <select v-model="formData.languages" multiple>
              <option value="chinese">中文</option>
              <option value="english">英文</option>
              <option value="japanese">日文</option>
              <option value="korean">韓文</option>
              <option value="spanish">西班牙文</option>
            </select>
            <small>按住 Ctrl/Cmd 可多選</small>
          </div>

          <div class="form-group">
            <label for="bio">個人簡介</label>
            <textarea id="bio" v-model.lazy="formData.bio" placeholder="請簡單介紹自己..." rows="4"></textarea>
          </div>
        </div>

        <!-- 表單按鈕 -->
        <div class="form-actions">
          <button type="submit" :disabled="!isFormValid || isSubmitting" class="submit-btn">
            {{ isSubmitting ? '提交中...' : '提交表單' }}
          </button>
          <button type="button" @click="resetForm" class="reset-btn">
            重置表單
          </button>
        </div>

        <!-- 提交訊息 -->
        <div v-if="submitMessage" class="submit-message" :class="{ 'success': submitMessage.includes('成功') }">
          {{ submitMessage }}
        </div>
      </form>

      <!-- 表單驗證狀態 -->
      <div class="validation-status">
        <h4>表單驗證狀態</h4>
        <div class="status-grid">
          <div class="status-item" :class="{ 'valid': formData.name.trim().length >= 2 }">
            <span class="status-icon">{{ formData.name.trim().length >= 2 ? '✅' : '❌' }}</span>
            <span>姓名驗證</span>
          </div>
          <div class="status-item" :class="{ 'valid': validateEmail(formData.email) }">
            <span class="status-icon">{{ validateEmail(formData.email) ? '✅' : '❌' }}</span>
            <span>Email驗證</span>
          </div>
          <div class="status-item" :class="{ 'valid': formData.age >= 18 && formData.age <= 100 }">
            <span class="status-icon">{{ formData.age >= 18 && formData.age <= 100 ? '✅' : '❌' }}</span>
                <span>年齡驗證</span>
          </div>
          <div class="status-item" :class="{ 'valid': formData.gender }">
            <span class="status-icon">{{ formData.gender ? '✅' : '❌' }}</span>
            <span>性別驗證</span>
          </div>
          <div class="status-item" :class="{ 'valid': formData.interests.length > 0 }">
            <span class="status-icon">{{ formData.interests.length > 0 ? '✅' : '❌' }}</span>
            <span>興趣驗證</span>
          </div>
        </div>
        <div class="overall-status" :class="{ 'valid': isFormValid }">
          整體狀態: {{ isFormValid ? '✅ 表單有效' : '❌ 表單無效' }}
        </div>
      </div>

      <!-- 表單摘要 -->
      <div class="form-summary">
        <h4>表單資料摘要</h4>
        <div class="summary-content">
          <div class="summary-item">
            <strong>姓名:</strong> {{ getFormSummary.name }}
          </div>
          <div class="summary-item">
            <strong>Email:</strong> {{ getFormSummary.email }}
          </div>
          <div class="summary-item">
            <strong>年齡:</strong> {{ getFormSummary.age }}
          </div>
          <div class="summary-item">
            <strong>性別:</strong> {{ getFormSummary.gender }}
          </div>
          <div class="summary-item">
            <strong>國家:</strong> {{ getFormSummary.country }}
          </div>
          <div class="summary-item">
            <strong>興趣:</strong> {{ getFormSummary.interests }}
          </div>
          <div class="summary-item">
            <strong>語言:</strong> {{ getFormSummary.languages }}
          </div>
          <div class="summary-item">
            <strong>簡介:</strong> {{ getFormSummary.bio }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 表單資料
const formData = ref({
  name: '',
  email: '',
  age: 18,
  gender: '',
  country: '',
  interests: [],
  languages: [],
  bio: ''
})

// 表單狀態
const isSubmitting = ref(false)
const submitMessage = ref('')

// 1. isFormValid (computed) - 計算表單整體驗證狀態
const isFormValid = computed(() => {
  const nameValid = formData.value.name.trim().length >= 2
  const emailValid = validateEmail(formData.value.email)
  const ageValid = formData.value.age >= 18 && formData.value.age <= 100
  const genderValid = formData.value.gender !== ''
  const interestsValid = formData.value.interests.length > 0

  return nameValid && emailValid && ageValid && genderValid && interestsValid
})

// 2. validateEmail(email) - 驗證 Email 格式
const validateEmail = (email) => {
  if (!email || email.trim() === '') return false
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  return emailRegex.test(email)
}

// 3. submitForm() - 處理表單提交邏輯
const submitForm = (event) => {
  event.preventDefault()

  if (!isFormValid.value) {
    submitMessage.value = '請完成所有必填欄位的正確填寫'
    return
  }

  isSubmitting.value = true
  submitMessage.value = ''

  // 模擬提交延遲
  setTimeout(() => {
    submitMessage.value = '表單提交成功！'
    isSubmitting.value = false
  }, 2000)
}

// 4. resetForm() - 重置表單為初始狀態
const resetForm = () => {
  formData.value = {
    name: '',
    email: '',
    age: 18,
    gender: '',
    country: '',
    interests: [],
    languages: [],
    bio: ''
  }
  submitMessage.value = ''
  isSubmitting.value = false
}

// 5. getFormSummary() (computed) - 生成表單資料摘要
const getFormSummary = computed(() => {
  return {
    name: formData.value.name || '未填寫',
    email: formData.value.email || '未填寫',
    age: formData.value.age || '未填寫',
    gender: formData.value.gender ?
      (formData.value.gender === 'male' ? '男性' :
        formData.value.gender === 'female' ? '女性' : '其他') : '未填寫',
    country: formData.value.country ?
      ({ taiwan: '台灣', china: '中國', japan: '日本', korea: '韓國', usa: '美國' }[formData.value.country] || formData.value.country) : '未填寫',
    interests: formData.value.interests.length > 0 ?
      formData.value.interests.map(interest =>
        ({ reading: '閱讀', music: '音樂', sports: '運動', travel: '旅遊', cooking: '烹飪' }[interest] || interest)
      ).join(', ') : '未填寫',
    languages: formData.value.languages.length > 0 ?
      formData.value.languages.map(lang =>
        ({ chinese: '中文', english: '英文', japanese: '日文', korean: '韓文', spanish: '西班牙文' }[lang] || lang)
      ).join(', ') : '未填寫',
    bio: formData.value.bio || '未填寫'
  }
})

// 6. handleAgeInput(event) - 處理年齡輸入的特殊邏輯
const handleAgeInput = (event) => {
  const value = parseInt(event.target.value)

  if (isNaN(value)) {
    return // 保持原值
  }

  // 範圍限制
  if (value < 1) {
    formData.value.age = 1
  } else if (value > 120) {
    formData.value.age = 120
  } else {
    formData.value.age = value
  }
}
</script>

<style scoped>
.self-challenge-solution {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.route-info {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  padding: 8px 16px;
  border-radius: 20px;
  font-size: 14px;
  display: inline-block;
  margin-bottom: 20px;
}

.form-container {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 30px;
  align-items: start;
}

.user-form {
  background: white;
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  border: 1px solid #e1e5e9;
}

.form-section {
  margin-bottom: 30px;
}

.form-section h4 {
  color: #2c3e50;
  margin-bottom: 20px;
  padding-bottom: 10px;
  border-bottom: 2px solid #3498db;
}

.form-group {
  margin-bottom: 20px;
}

.form-group label {
  display: block;
  margin-bottom: 8px;
  font-weight: 600;
  color: #2c3e50;
}

.form-group input,
.form-group select,
.form-group textarea {
  width: 100%;
  padding: 12px;
  border: 2px solid #e1e5e9;
  border-radius: 8px;
  font-size: 14px;
  transition: all 0.3s ease;
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #3498db;
  box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
}

.form-group input.error,
.form-group select.error,
.form-group textarea.error {
  border-color: #e74c3c;
  box-shadow: 0 0 0 3px rgba(231, 76, 60, 0.1);
}

.error-text {
  color: #e74c3c;
  font-size: 12px;
  margin-top: 5px;
  display: block;
}

.radio-group,
.checkbox-group {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
}

.radio-label,
.checkbox-label {
  display: flex;
  align-items: center;
  cursor: pointer;
  font-weight: normal !important;
}

.radio-label input,
.checkbox-label input {
  width: auto;
  margin-right: 8px;
}

.form-group select[multiple] {
  height: 120px;
}

.form-group small {
  color: #7f8c8d;
  font-size: 12px;
  margin-top: 5px;
  display: block;
}

.form-actions {
  display: flex;
  gap: 15px;
  margin-top: 30px;
}

.submit-btn,
.reset-btn {
  padding: 12px 30px;
  border: none;
  border-radius: 8px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.submit-btn {
  background: linear-gradient(135deg, #3498db, #2980b9);
  color: white;
}

.submit-btn:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 5px 15px rgba(52, 152, 219, 0.3);
}

.submit-btn:disabled {
  background: #bdc3c7;
  cursor: not-allowed;
}

.reset-btn {
  background: #ecf0f1;
  color: #2c3e50;
}

.reset-btn:hover {
  background: #d5dbdb;
}

.submit-message {
  margin-top: 20px;
  padding: 15px;
  border-radius: 8px;
  font-weight: 600;
  text-align: center;
}

.submit-message.success {
  background: #d5f4e6;
  color: #27ae60;
  border: 1px solid #27ae60;
}

.validation-status {
  background: white;
  padding: 25px;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  border: 1px solid #e1e5e9;
}

.validation-status h4 {
  color: #2c3e50;
  margin-bottom: 20px;
  text-align: center;
}

.status-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 10px;
  margin-bottom: 20px;
}

.status-item {
  display: flex;
  align-items: center;
  padding: 10px;
  border-radius: 8px;
  background: #f8f9fa;
  transition: all 0.3s ease;
}

.status-item.valid {
  background: #d5f4e6;
  border-left: 4px solid #27ae60;
}

.status-icon {
  margin-right: 10px;
  font-size: 16px;
}

.overall-status {
  text-align: center;
  padding: 15px;
  border-radius: 8px;
  font-weight: 600;
  background: #f8f9fa;
}

.overall-status.valid {
  background: #d5f4e6;
  color: #27ae60;
}

.form-summary {
  grid-column: 1 / -1;
  background: white;
  padding: 25px;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
  border: 1px solid #e1e5e9;
  margin-top: 20px;
}

.form-summary h4 {
  color: #2c3e50;
  margin-bottom: 20px;
  text-align: center;
}

.summary-content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 15px;
}

.summary-item {
  padding: 10px;
  background: #f8f9fa;
  border-radius: 8px;
  border-left: 4px solid #3498db;
}

.summary-item strong {
  color: #2c3e50;
}

@media (max-width: 768px) {
  .form-container {
    grid-template-columns: 1fr;
  }

  .form-actions {
    flex-direction: column;
  }

  .summary-content {
    grid-template-columns: 1fr;
  }
}
</style>
