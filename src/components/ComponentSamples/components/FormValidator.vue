<template>
    <div class="form-validator">
        <div class="form-section">
            <h5>表單驗證範例</h5>
            <form @submit.prevent="submitForm" class="validation-form">
                <div class="field-group">
                    <label>電子郵件:</label>
                    <input v-model="formData.email" type="email" :class="['input-field', getFieldClass('email')]"
                        placeholder="請輸入電子郵件">
                    <span v-if="errors.email" class="error-msg">{{ errors.email }}</span>
                </div>

                <div class="field-group">
                    <label>密碼:</label>
                    <input v-model="formData.password" type="password"
                        :class="['input-field', getFieldClass('password')]" placeholder="請輸入密碼">
                    <span v-if="errors.password" class="error-msg">{{ errors.password }}</span>
                </div>

                <div class="field-group">
                    <label>年齡:</label>
                    <input v-model.number="formData.age" type="number" :class="['input-field', getFieldClass('age')]"
                        placeholder="請輸入年齡">
                    <span v-if="errors.age" class="error-msg">{{ errors.age }}</span>
                </div>

                <div class="form-actions">
                    <button type="submit" class="btn btn-primary">
                        提交表單
                    </button>
                    <button type="button" @click="resetForm" class="btn btn-secondary">
                        重置
                    </button>
                </div>
            </form>
        </div>

        <div class="validation-info">
            <h6>驗證規則:</h6>
            <ul>
                <li>電子郵件必須為有效格式</li>
                <li>密碼長度至少6個字符</li>
                <li>年齡必須在18-100之間</li>
            </ul>
        </div>
    </div>
</template>

<script setup>
import { ref, reactive } from 'vue'

const emit = defineEmits({
    'form-submitted': (payload) => {
        // 驗證事件參數
        if (!payload || typeof payload !== 'object') return false
        if (!payload.status) return false
        return ['success', 'error'].includes(payload.status)
    }
})

const formData = reactive({
    email: '',
    password: '',
    age: null
})

const errors = ref({})

const validateForm = () => {
    const newErrors = {}

    // 驗證電子郵件
    if (!formData.email) {
        newErrors.email = '電子郵件為必填項'
    } else if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(formData.email)) {
        newErrors.email = '請輸入有效的電子郵件格式'
    }

    // 驗證密碼
    if (!formData.password) {
        newErrors.password = '密碼為必填項'
    } else if (formData.password.length < 6) {
        newErrors.password = '密碼長度至少需要6個字符'
    }

    // 驗證年齡
    if (!formData.age) {
        newErrors.age = '年齡為必填項'
    } else if (formData.age < 18 || formData.age > 100) {
        newErrors.age = '年齡必須在18-100之間'
    }

    errors.value = newErrors

    return {
        isValid: Object.keys(newErrors).length === 0,
        message: Object.keys(newErrors).length === 0 ? '表單驗證通過' : '表單驗證失敗',
        errors: newErrors
    }
}

const getFieldClass = (field) => {
    if (errors.value[field]) return 'error'
    if (formData[field] && !errors.value[field]) return 'success'
    return ''
}

const submitForm = () => {
    const result = validateForm()

    emit('form-submitted', {
        status: result.isValid ? 'success' : 'error',
        message: result.message,
        data: result.isValid ? { ...formData } : null,
        errors: result.errors
    })
}

const resetForm = () => {
    formData.email = ''
    formData.password = ''
    formData.age = null
    errors.value = {}
}
</script>
