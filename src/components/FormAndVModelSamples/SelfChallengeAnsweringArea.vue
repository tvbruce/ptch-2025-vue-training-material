<template>
    <div class="answering-area">
        <h2>🎯 實作練習區 - 表單輸入與 v-model</h2>
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
                    <input v-model.number="formData.age" type="number" placeholder="請輸入年齡" class="form-input" min="0"
                        max="120">
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
                    <textarea v-model="formData.bio" placeholder="請簡單介紹一下自己..." class="form-textarea"
                        rows="4"></textarea>
                    <div class="char-count">{{ formData.bio.length }} / 500 字</div>
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
                    <div class="status-item"
                        :class="{ 'valid': !errors.confirmPassword, 'invalid': errors.confirmPassword }">
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

// 🎯 任務：實作 validateUsername 方法
// eslint-disable-next-line no-unused-vars
const validateUsername = () => {
    // 請在這裡實作使用者名稱驗證邏輯
    // 要求：3-20字元，只能包含字母、數字、底線
    console.log('請實作使用者名稱驗證功能')
}

// 🎯 任務：實作 validateEmail 方法
// eslint-disable-next-line no-unused-vars
const validateEmail = () => {
    // 請在這裡實作電子郵件驗證邏輯
    // 要求：符合電子郵件格式
    console.log('請實作電子郵件驗證功能')
}

// 🎯 任務：實作 validatePassword 方法
// eslint-disable-next-line no-unused-vars
const validatePassword = () => {
    // 請在這裡實作密碼驗證邏輯
    // 要求：至少8字元，包含大小寫字母和數字
    console.log('請實作密碼驗證功能')
}

// 🎯 任務：實作 validateConfirmPassword 方法
// eslint-disable-next-line no-unused-vars
const validateConfirmPassword = () => {
    // 請在這裡實作確認密碼驗證邏輯
    // 要求：必須與密碼相同
    console.log('請實作確認密碼驗證功能')
}

// 🎯 任務：實作 validateForm 方法
const validateForm = () => {
    // 請在這裡實作完整表單驗證邏輯
    // 呼叫所有驗證方法
    console.log('請實作表單驗證功能')
}

// 🎯 任務：實作 isFormValid 計算屬性
const isFormValid = computed(() => {
    // 請在這裡實作表單有效性檢查
    // 檢查所有必要欄位都已填寫且無錯誤
    return false
})

// 🎯 任務：實作 formDataPreview 計算屬性
const formDataPreview = computed(() => {
    // 請在這裡實作表單資料格式化預覽
    // 將 formData 格式化為易讀的 JSON 字串
    return JSON.stringify(formData.value, null, 2)
})

// 🎯 任務：實作 submitForm 方法
const submitForm = async () => {
    // 請在這裡實作表單提交邏輯
    // 1. 最終驗證
    // 2. 模擬 API 提交
    // 3. 顯示結果訊息
    console.log('請實作表單提交功能')
}

// 🎯 任務：實作 resetForm 方法
const resetForm = () => {
    // 請在這裡實作表單重置邏輯
    // 將所有欄位重置為初始值
    console.log('請實作表單重置功能')
}

// 🎯 任務：實作 fillSampleData 方法
const fillSampleData = () => {
    // 請在這裡實作填入範例資料的邏輯
    // 填入一組測試資料方便開發測試
    console.log('請實作填入範例資料功能')
}

// 🎯 任務：實作 watch 監聽器
// 監聽表單欄位變化進行即時驗證
watch(() => formData.value.username, () => {
    // 監聽使用者名稱變化
    console.log('請實作使用者名稱即時驗證')
})

watch(() => formData.value.email, () => {
    // 監聽電子郵件變化
    console.log('請實作電子郵件即時驗證')
})

watch(() => formData.value.password, () => {
    // 監聽密碼變化
    console.log('請實作密碼即時驗證')
})

watch(() => formData.value.confirmPassword, () => {
    // 監聽確認密碼變化
    console.log('請實作確認密碼即時驗證')
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
    transition: background-color 0.3s ease;
}

.btn:disabled {
    opacity: 0.6;
    cursor: not-allowed;
}

.btn-primary {
    background: #007bff;
    color: white;
}

.btn-secondary {
    background: #6c757d;
    color: white;
}

.btn-success {
    background: #28a745;
    color: white;
}

.btn-info {
    background: #17a2b8;
    color: white;
}

.btn:hover:not(:disabled) {
    opacity: 0.9;
}

.submit-message {
    margin-top: 1rem;
    padding: 1rem;
    border-radius: 4px;
    font-weight: bold;
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
