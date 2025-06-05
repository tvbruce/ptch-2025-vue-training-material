<template>
    <div class="task-form">
        <h4>📝 新增任務表單</h4>

        <form @submit.prevent="handleSubmit" class="form">
            <!-- 任務標題 -->
            <div class="form-group">
                <label for="title">任務標題 *</label>
                <input id="title" v-model="formData.title" type="text" class="form-input"
                    :class="{ 'error': errors.title }" placeholder="請輸入任務標題" required />
                <span v-if="errors.title" class="error-text">{{ errors.title }}</span>
            </div>

            <!-- 任務描述 -->
            <div class="form-group">
                <label for="description">任務描述</label>
                <textarea id="description" v-model="formData.description" class="form-input" placeholder="請輸入任務描述"
                    rows="3" maxlength="200"></textarea>
                <div class="char-count">{{ formData.description.length }} / 200 字</div>
            </div>

            <!-- 優先級 -->
            <div class="form-group">
                <label for="priority">優先級</label>
                <select id="priority" v-model="formData.priority" class="form-input">
                    <option value="low">低優先級</option>
                    <option value="medium">中優先級</option>
                    <option value="high">高優先級</option>
                </select>
            </div>

            <!-- 表單按鈕 -->
            <div class="form-actions">
                <button type="submit" class="btn btn-primary" :disabled="!isFormValid || isSubmitting">
                    {{ isSubmitting ? '新增中...' : '新增任務' }}
                </button>
                <button type="button" @click="resetForm" class="btn btn-secondary">
                    重置
                </button>
            </div>
        </form>

        <!-- 表單預覽 -->
        <div v-if="formData.title" class="form-preview">
            <h5>📋 任務預覽</h5>
            <div class="preview-content">
                <p><strong>標題：</strong>{{ formData.title }}</p>
                <p><strong>描述：</strong>{{ formData.description || '無' }}</p>
                <p><strong>優先級：</strong>{{ priorityText }}</p>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, reactive } from 'vue'

// 定義 emit 事件
const emit = defineEmits(['add-task'])

// 表單資料
const formData = reactive({
    title: '',
    description: '',
    priority: 'medium'
})

// 錯誤訊息
const errors = reactive({
    title: ''
})

// 提交狀態
const isSubmitting = ref(false)

// 計算屬性
const priorityText = computed(() => {
    const priorityMap = {
        high: '高優先級',
        medium: '中優先級',
        low: '低優先級'
    }
    return priorityMap[formData.priority] || '未知'
})

const isFormValid = computed(() => {
    return formData.title.trim().length >= 2 && !errors.title
})

// 驗證表單
const validateForm = () => {
    errors.title = ''

    if (!formData.title.trim()) {
        errors.title = '任務標題不能為空'
        return false
    }

    if (formData.title.trim().length < 2) {
        errors.title = '任務標題至少需要2個字元'
        return false
    }

    if (formData.title.trim().length > 50) {
        errors.title = '任務標題不能超過50個字元'
        return false
    }

    return true
}

// 表單提交處理
const handleSubmit = async () => {
    if (!validateForm()) return

    isSubmitting.value = true

    try {
        // 模擬提交延遲
        await new Promise(resolve => setTimeout(resolve, 500))

        // 發送事件給父組件
        emit('add-task', {
            title: formData.title.trim(),
            description: formData.description.trim(),
            priority: formData.priority
        })

        // 重置表單
        resetForm()

    } catch (error) {
        console.error('提交失敗:', error)
    } finally {
        isSubmitting.value = false
    }
}

// 重置表單
const resetForm = () => {
    formData.title = ''
    formData.description = ''
    formData.priority = 'medium'
    errors.title = ''
}
</script>

<style scoped>
.task-form {
    background: white;
    border-radius: 8px;
    padding: 1.5rem;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.task-form h4 {
    margin: 0 0 1.5rem 0;
    color: #495057;
    text-align: center;
}

.form {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
}

.form-group {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}

.form-group label {
    font-weight: bold;
    color: #495057;
}

.form-input {
    padding: 0.75rem;
    border: 2px solid #dee2e6;
    border-radius: 4px;
    font-size: 1rem;
    transition: all 0.3s ease;
}

.form-input:focus {
    outline: none;
    border-color: #20c997;
    box-shadow: 0 0 0 3px rgba(32, 201, 151, 0.1);
}

.form-input.error {
    border-color: #dc3545;
}

.form-input.error:focus {
    box-shadow: 0 0 0 3px rgba(220, 53, 69, 0.1);
}

.error-text {
    color: #dc3545;
    font-size: 0.875rem;
    margin-top: 0.25rem;
}

.char-count {
    font-size: 0.875rem;
    color: #6c757d;
    text-align: right;
}

.form-actions {
    display: flex;
    gap: 1rem;
    margin-top: 1rem;
}

.btn {
    padding: 0.75rem 1.5rem;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 1rem;
    font-weight: 500;
    transition: all 0.3s ease;
    min-width: 120px;
}

.btn:disabled {
    opacity: 0.6;
    cursor: not-allowed;
}

.btn-primary {
    background: #20c997;
    color: white;
}

.btn-primary:hover:not(:disabled) {
    background: #1bae87;
    transform: translateY(-1px);
}

.btn-secondary {
    background: #6c757d;
    color: white;
}

.btn-secondary:hover {
    background: #545b62;
    transform: translateY(-1px);
}

.form-preview {
    margin-top: 1.5rem;
    padding: 1rem;
    background: #e8f5f0;
    border-radius: 8px;
    border-left: 4px solid #20c997;
}

.form-preview h5 {
    margin: 0 0 1rem 0;
    color: #495057;
    font-size: 1rem;
}

.preview-content {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}

.preview-content p {
    margin: 0;
    color: #495057;
    font-size: 0.9rem;
}

.preview-content strong {
    color: #20c997;
}

@media (max-width: 768px) {
    .form-actions {
        flex-direction: column;
    }

    .btn {
        width: 100%;
    }
}
</style>
