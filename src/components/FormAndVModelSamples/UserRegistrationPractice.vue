<template>
  <div class="user-registration-practice">
    <h2>📝 用戶註冊表單 - v-model 練習</h2>
    <p class="route-info">📍 路徑：/FormAndVModelSamples/UserRegistrationPractice.vue</p>
    <p class="description">
      📝 <strong>練習目標：</strong>學習 v-model 在各種表單元素中的使用，掌握雙向數據綁定
    </p>

    <div class="demo-section">
      <h3>🎯 練習任務</h3>
      <div class="task-list">
        <div class="task-item">
          <span>✅ 1. 文本輸入與 v-model</span>
        </div>
        <div class="task-item">
          <span>✅ 2. 單選按鈕與 v-model</span>
        </div>
        <div class="task-item">
          <span>✅ 3. 多選框與 v-model</span>
        </div>
        <div class="task-item">
          <span>✅ 4. 下拉選單與 v-model</span>
        </div>
        <div class="task-item">
          <span>✅ 5. 表單驗證與即時反饋</span>
        </div>
      </div>
    </div>

    <div class="demo-section">
      <h3>👤 註冊表單</h3>
      <form @submit.prevent="handleSubmit" class="registration-form">
        <!-- 基本資訊 -->
        <div class="form-section">
          <h4>基本資訊</h4>
          <div class="form-row">
            <div class="form-group">
              <label for="username">用戶名 *</label>
              <input id="username" v-model="form.username" type="text" class="input-field"
                :class="{ 'error': errors.username }" placeholder="請輸入用戶名" @blur="validateUsername">
              <div v-if="errors.username" class="error-message">
                {{ errors.username }}
              </div>
            </div>
            <div class="form-group">
              <label for="email">電子郵箱 *</label>
              <input id="email" v-model="form.email" type="email" class="input-field" :class="{ 'error': errors.email }"
                placeholder="example@email.com" @blur="validateEmail">
              <div v-if="errors.email" class="error-message">
                {{ errors.email }}
              </div>
            </div>
          </div>

          <div class="form-row">
            <div class="form-group">
              <label for="password">密碼 *</label>
              <input id="password" v-model="form.password" type="password" class="input-field"
                :class="{ 'error': errors.password }" placeholder="至少 6 個字符" @input="validatePassword">
              <div class="password-strength">
                <div class="strength-bar">
                  <div class="strength-fill" :class="passwordStrength.class"
                    :style="{ width: passwordStrength.width + '%' }"></div>
                </div>
                <span class="strength-text">{{ passwordStrength.text }}</span>
              </div>
              <div v-if="errors.password" class="error-message">
                {{ errors.password }}
              </div>
            </div>
            <div class="form-group">
              <label for="confirmPassword">確認密碼 *</label>
              <input id="confirmPassword" v-model="form.confirmPassword" type="password" class="input-field"
                :class="{ 'error': errors.confirmPassword }" placeholder="再次輸入密碼" @blur="validateConfirmPassword">
              <div v-if="errors.confirmPassword" class="error-message">
                {{ errors.confirmPassword }}
              </div>
            </div>
          </div>
        </div>

        <!-- 個人資訊 -->
        <div class="form-section">
          <h4>個人資訊</h4>
          <div class="form-row">
            <div class="form-group">
              <label>性別</label>
              <div class="radio-group">
                <label class="radio-label">
                  <input v-model="form.gender" type="radio" value="male">
                  <span>男性</span>
                </label>
                <label class="radio-label">
                  <input v-model="form.gender" type="radio" value="female">
                  <span>女性</span>
                </label>
                <label class="radio-label">
                  <input v-model="form.gender" type="radio" value="other">
                  <span>其他</span>
                </label>
              </div>
            </div>
            <div class="form-group">
              <label for="birthDate">出生日期</label>
              <input id="birthDate" v-model="form.birthDate" type="date" class="input-field">
            </div>
          </div>

          <div class="form-row">
            <div class="form-group">
              <label for="country">國家/地區</label>
              <select id="country" v-model="form.country" class="select-field">
                <option value="">請選擇國家</option>
                <option value="taiwan">台灣</option>
                <option value="china">中國</option>
                <option value="hongkong">香港</option>
                <option value="singapore">新加坡</option>
                <option value="japan">日本</option>
                <option value="korea">韓國</option>
                <option value="usa">美國</option>
                <option value="other">其他</option>
              </select>
            </div>
            <div class="form-group">
              <label for="occupation">職業</label>
              <select id="occupation" v-model="form.occupation" class="select-field">
                <option value="">請選擇職業</option>
                <option value="student">學生</option>
                <option value="engineer">工程師</option>
                <option value="designer">設計師</option>
                <option value="teacher">教師</option>
                <option value="doctor">醫生</option>
                <option value="business">商業人士</option>
                <option value="other">其他</option>
              </select>
            </div>
          </div>
        </div>

        <!-- 興趣愛好 -->
        <div class="form-section">
          <h4>興趣愛好 (可多選)</h4>
          <div class="checkbox-group">
            <label v-for="hobby in hobbiesList" :key="hobby.value" class="checkbox-label">
              <input v-model="form.hobbies" type="checkbox" :value="hobby.value">
              <span>{{ hobby.label }}</span>
            </label>
          </div>
        </div>

        <!-- 其他設定 -->
        <div class="form-section">
          <h4>其他設定</h4>
          <div class="form-group">
            <label for="bio">個人簡介</label>
            <textarea id="bio" v-model="form.bio" class="textarea-field" placeholder="簡單介紹一下自己..." rows="4"></textarea>
            <div class="char-count">
              {{ form.bio.length }}/500 字符
            </div>
          </div>

          <div class="checkbox-group">
            <label class="checkbox-label">
              <input v-model="form.newsletter" type="checkbox">
              <span>訂閱電子報</span>
            </label>
            <label class="checkbox-label">
              <input v-model="form.terms" type="checkbox">
              <span>我同意 <a href="#" @click.prevent>服務條款</a> *</span>
            </label>
          </div>
        </div>

        <div class="form-actions">
          <button type="submit" class="btn btn-primary btn-large" :disabled="!isFormValid">
            註冊
          </button>
          <button type="button" @click="resetForm" class="btn btn-secondary btn-large">
            重置
          </button>
        </div>
      </form>
    </div>

    <!-- 預覽區域 -->
    <div class="demo-section">
      <h3>👁️ 表單數據預覽</h3>
      <div class="form-preview">
        <pre>{{ JSON.stringify(form, null, 2) }}</pre>
      </div>
    </div>

    <div class="code-example">
      <h4>💻 關鍵代碼</h4>
      <pre v-pre><code>// 基本 v-model 用法
&lt;input v-model="form.username" type="text"&gt;

// 單選按鈕
&lt;input v-model="form.gender" type="radio" value="male"&gt;
&lt;input v-model="form.gender" type="radio" value="female"&gt;

// 多選框
&lt;input v-model="form.hobbies" type="checkbox" value="reading"&gt;
&lt;input v-model="form.hobbies" type="checkbox" value="sports"&gt;

// 下拉選單
&lt;select v-model="form.country"&gt;
  &lt;option value="taiwan"&gt;台灣&lt;/option&gt;
  &lt;option value="china"&gt;中國&lt;/option&gt;
&lt;/select&gt;

// 文本域
&lt;textarea v-model="form.bio"&gt;&lt;/textarea&gt;

// 響應式數據
const form = ref({
  username: '',
  email: '',
  gender: '',
  hobbies: [],
  country: '',
  bio: ''
})</code></pre>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 表單數據
const form = ref({
  username: '',
  email: '',
  password: '',
  confirmPassword: '',
  gender: '',
  birthDate: '',
  country: '',
  occupation: '',
  hobbies: [],
  bio: '',
  newsletter: false,
  terms: false
})

// 錯誤狀態
const errors = ref({
  username: '',
  email: '',
  password: '',
  confirmPassword: ''
})

// 興趣列表
const hobbiesList = [
  { value: 'reading', label: '📚 閱讀' },
  { value: 'sports', label: '⚽ 運動' },
  { value: 'music', label: '🎵 音樂' },
  { value: 'travel', label: '✈️ 旅行' },
  { value: 'gaming', label: '🎮 遊戲' },
  { value: 'cooking', label: '🍳 烹飪' },
  { value: 'photography', label: '📷 攝影' },
  { value: 'art', label: '🎨 藝術' }
]

// 密碼強度計算
const passwordStrength = computed(() => {
  const password = form.value.password
  let score = 0

  if (password.length >= 6) score += 1
  if (password.length >= 8) score += 1
  if (/[A-Z]/.test(password)) score += 1
  if (/[0-9]/.test(password)) score += 1
  if (/[^A-Za-z0-9]/.test(password)) score += 1

  switch (score) {
    case 0:
    case 1:
      return { width: 20, class: 'weak', text: '弱' }
    case 2:
      return { width: 40, class: 'fair', text: '一般' }
    case 3:
      return { width: 60, class: 'good', text: '良好' }
    case 4:
      return { width: 80, class: 'strong', text: '強' }
    case 5:
      return { width: 100, class: 'very-strong', text: '很強' }
    default:
      return { width: 0, class: '', text: '' }
  }
})

// 表單驗證
const isFormValid = computed(() => {
  return form.value.username.trim() !== '' &&
    form.value.email.trim() !== '' &&
    form.value.password.length >= 6 &&
    form.value.password === form.value.confirmPassword &&
    form.value.terms &&
    !Object.values(errors.value).some(error => error !== '')
})

// 驗證函數
const validateUsername = () => {
  if (!form.value.username.trim()) {
    errors.value.username = '用戶名不能為空'
  } else if (form.value.username.length < 3) {
    errors.value.username = '用戶名至少需要 3 個字符'
  } else {
    errors.value.username = ''
  }
}

const validateEmail = () => {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  if (!form.value.email.trim()) {
    errors.value.email = '電子郵箱不能為空'
  } else if (!emailRegex.test(form.value.email)) {
    errors.value.email = '請輸入有效的電子郵箱'
  } else {
    errors.value.email = ''
  }
}

const validatePassword = () => {
  if (form.value.password.length < 6) {
    errors.value.password = '密碼至少需要 6 個字符'
  } else {
    errors.value.password = ''
  }
  // 同時驗證確認密碼
  validateConfirmPassword()
}

const validateConfirmPassword = () => {
  if (form.value.confirmPassword !== form.value.password) {
    errors.value.confirmPassword = '兩次輸入的密碼不一致'
  } else {
    errors.value.confirmPassword = ''
  }
}

// 提交處理
const handleSubmit = () => {
  // 執行所有驗證
  validateUsername()
  validateEmail()
  validatePassword()
  validateConfirmPassword()

  if (isFormValid.value) {
    alert('註冊成功！\n\n查看控制台了解提交的數據')
    console.log('提交的表單數據：', form.value)
  } else {
    alert('請檢查表單中的錯誤信息')
  }
}

// 重置表單
const resetForm = () => {
  form.value = {
    username: '',
    email: '',
    password: '',
    confirmPassword: '',
    gender: '',
    birthDate: '',
    country: '',
    occupation: '',
    hobbies: [],
    bio: '',
    newsletter: false,
    terms: false
  }

  errors.value = {
    username: '',
    email: '',
    password: '',
    confirmPassword: ''
  }
}
</script>
