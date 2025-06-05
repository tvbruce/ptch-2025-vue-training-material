<template>
    <div class="task-form">
        <h4>➕ 新增任務</h4>
        <form @submit.prevent="handleSubmit" class="form">
            <div class="form-group">
                <label for="title">任務標題 *</label>
                <input id="title" v-model="formData.title" type="text" placeholder="輸入任務標題" required>
            </div>

            <div class="form-group">
                <label for="description">任務描述</label>
                <textarea id="description" v-model="formData.description" placeholder="輸入任務描述" rows="3"></textarea>
            </div>

            <div class="form-row">
                <div class="form-group">
                    <label for="priority">優先級</label>
                    <select id="priority" v-model="formData.priority">
                        <option value="low">低</option>
                        <option value="medium">中</option>
                        <option value="high">高</option>
                    </select>
                </div>

                <div class="form-group">
                    <label for="dueDate">截止日期</label>
                    <input id="dueDate" v-model="formData.dueDate" type="date">
                </div>
            </div>

            <div class="form-actions">
                <button type="submit" class="submit-btn" :disabled="!formData.title.trim()">
                    ✅ 新增任務
                </button>
                <button type="button" @click="resetForm" class="reset-btn">
                    🔄 重置
                </button>
            </div>
        </form>
    </div>
</template>

<script setup>
import { ref } from 'vue'

// 定義事件
const emit = defineEmits(['add-task'])

// 表單資料
const formData = ref({
    title: '',
    description: '',
    priority: 'medium',
    dueDate: ''
})

// 處理表單提交
const handleSubmit = () => {
    if (!formData.value.title.trim()) return

    const newTask = {
        title: formData.value.title.trim(),
        description: formData.value.description.trim(),
        priority: formData.value.priority,
        dueDate: formData.value.dueDate ? new Date(formData.value.dueDate) : null
    }

    emit('add-task', newTask)
    resetForm()
}

// 重置表單
const resetForm = () => {
    formData.value = {
        title: '',
        description: '',
        priority: 'medium',
        dueDate: ''
    }
}
</script>

<style scoped>
.task-form {
    background: white;
    padding: 20px;
    border-radius: 15px;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
    border: 1px solid #e1e5e9;
    margin-bottom: 20px;
}

.task-form h4 {
    color: #2c3e50;
    margin-bottom: 20px;
    text-align: center;
}

.form {
    display: grid;
    gap: 15px;
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
    margin-bottom: 5px;
}

.form-group input,
.form-group select,
.form-group textarea {
    padding: 10px;
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
}

.form-group textarea {
    resize: vertical;
    min-height: 80px;
}

.form-actions {
    display: flex;
    gap: 10px;
    margin-top: 10px;
}

.submit-btn,
.reset-btn {
    flex: 1;
    padding: 12px;
    border: none;
    border-radius: 8px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
}

.submit-btn {
    background: linear-gradient(135deg, #27ae60, #2ecc71);
    color: white;
}

.submit-btn:hover:not(:disabled) {
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(39, 174, 96, 0.3);
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

@media (max-width: 768px) {
    .form-row {
        grid-template-columns: 1fr;
    }

    .form-actions {
        flex-direction: column;
    }
}
</style>
