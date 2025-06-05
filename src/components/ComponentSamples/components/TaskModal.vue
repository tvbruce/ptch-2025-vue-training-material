<template>
    <div class="modal-overlay" @click="handleOverlayClick">
        <div class="modal-content" @click.stop>
            <div class="modal-header">
                <h3>✏️ 編輯任務</h3>
                <button @click="$emit('close')" class="close-btn">✕</button>
            </div>

            <form @submit.prevent="handleSubmit" class="modal-form">
                <div class="form-group">
                    <label for="editTitle">任務標題 *</label>
                    <input id="editTitle" v-model="formData.title" type="text" placeholder="輸入任務標題" required>
                </div>

                <div class="form-group">
                    <label for="editDescription">任務描述</label>
                    <textarea id="editDescription" v-model="formData.description" placeholder="輸入任務描述"
                        rows="4"></textarea>
                </div>

                <div class="form-row">
                    <div class="form-group">
                        <label for="editPriority">優先級</label>
                        <select id="editPriority" v-model="formData.priority">
                            <option value="low">低</option>
                            <option value="medium">中</option>
                            <option value="high">高</option>
                        </select>
                    </div>

                    <div class="form-group">
                        <label for="editDueDate">截止日期</label>
                        <input id="editDueDate" v-model="formData.dueDate" type="date">
                    </div>
                </div>

                <div class="form-group">
                    <label class="checkbox-group">
                        <input type="checkbox" v-model="formData.completed">
                        <span class="checkbox-label">任務已完成</span>
                    </label>
                </div>

                <div class="modal-actions">
                    <button type="button" @click="$emit('close')" class="cancel-btn">
                        取消
                    </button>
                    <button type="submit" class="save-btn" :disabled="!formData.title.trim()">
                        💾 保存變更
                    </button>
                </div>
            </form>
        </div>
    </div>
</template>

<script setup>
import { ref, watch } from 'vue'

// 定義 props
const props = defineProps({
    task: {
        type: Object,
        required: true
    }
})

// 定義事件
const emit = defineEmits(['close', 'save'])

// 表單資料
const formData = ref({
    id: '',
    title: '',
    description: '',
    priority: 'medium',
    dueDate: '',
    completed: false,
    createdAt: null
})

// 監聽 task prop 變化，更新表單資料
watch(() => props.task, (newTask) => {
    if (newTask) {
        formData.value = {
            id: newTask.id,
            title: newTask.title || '',
            description: newTask.description || '',
            priority: newTask.priority || 'medium',
            dueDate: newTask.dueDate ? formatDateForInput(newTask.dueDate) : '',
            completed: newTask.completed || false,
            createdAt: newTask.createdAt
        }
    }
}, { immediate: true })

// 處理表單提交
const handleSubmit = () => {
    if (!formData.value.title.trim()) return

    const updatedTask = {
        ...formData.value,
        title: formData.value.title.trim(),
        description: formData.value.description.trim(),
        dueDate: formData.value.dueDate ? new Date(formData.value.dueDate) : null
    }

    emit('save', updatedTask)
}

// 處理遮罩點擊
const handleOverlayClick = (event) => {
    if (event.target === event.currentTarget) {
        emit('close')
    }
}

// 格式化日期為輸入框格式
const formatDateForInput = (date) => {
    if (!date) return ''
    const d = new Date(date)
    return d.toISOString().split('T')[0]
}
</script>

<style scoped>
.modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000;
    padding: 20px;
}

.modal-content {
    background: white;
    border-radius: 15px;
    box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
    width: 100%;
    max-width: 500px;
    max-height: 90vh;
    overflow-y: auto;
    animation: modalSlideIn 0.3s ease-out;
}

@keyframes modalSlideIn {
    from {
        opacity: 0;
        transform: translateY(-50px) scale(0.9);
    }

    to {
        opacity: 1;
        transform: translateY(0) scale(1);
    }
}

.modal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px 25px;
    border-bottom: 1px solid #e1e5e9;
}

.modal-header h3 {
    margin: 0;
    color: #2c3e50;
    font-size: 1.3rem;
}

.close-btn {
    width: 32px;
    height: 32px;
    border: none;
    background: #f8f9fa;
    border-radius: 50%;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 16px;
    color: #7f8c8d;
    transition: all 0.3s ease;
}

.close-btn:hover {
    background: #e9ecef;
    color: #2c3e50;
    transform: scale(1.1);
}

.modal-form {
    padding: 25px;
    display: grid;
    gap: 20px;
}

.form-group {
    display: flex;
    flex-direction: column;
}

.form-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 15px;
}

.form-group label {
    font-weight: 600;
    color: #2c3e50;
    margin-bottom: 8px;
}

.form-group input,
.form-group select,
.form-group textarea {
    padding: 12px;
    border: 2px solid #e1e5e9;
    border-radius: 8px;
    font-size: 14px;
    transition: border-color 0.3s ease;
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
    outline: none;
    border-color: #3498db;
    box-shadow: 0 0 0 3px rgba(52, 152, 219, 0.1);
}

.form-group textarea {
    resize: vertical;
    min-height: 100px;
}

.checkbox-group {
    display: flex !important;
    flex-direction: row !important;
    align-items: center;
    cursor: pointer;
    padding: 12px;
    background: #f8f9fa;
    border-radius: 8px;
    transition: background 0.3s ease;
}

.checkbox-group:hover {
    background: #e9ecef;
}

.checkbox-group input[type="checkbox"] {
    margin-right: 10px;
    width: 18px;
    height: 18px;
    cursor: pointer;
}

.checkbox-label {
    font-weight: 500 !important;
    margin: 0 !important;
    cursor: pointer;
}

.modal-actions {
    display: flex;
    gap: 12px;
    margin-top: 10px;
}

.cancel-btn,
.save-btn {
    flex: 1;
    padding: 12px 20px;
    border: none;
    border-radius: 8px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
}

.cancel-btn {
    background: #ecf0f1;
    color: #2c3e50;
}

.cancel-btn:hover {
    background: #d5dbdb;
}

.save-btn {
    background: linear-gradient(135deg, #3498db, #2980b9);
    color: white;
}

.save-btn:hover:not(:disabled) {
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(52, 152, 219, 0.3);
}

.save-btn:disabled {
    background: #bdc3c7;
    cursor: not-allowed;
    transform: none;
    box-shadow: none;
}

@media (max-width: 768px) {
    .modal-overlay {
        padding: 10px;
    }

    .modal-content {
        max-height: 95vh;
    }

    .modal-header {
        padding: 15px 20px;
    }

    .modal-form {
        padding: 20px;
    }

    .form-row {
        grid-template-columns: 1fr;
    }

    .modal-actions {
        flex-direction: column;
    }
}
</style>
