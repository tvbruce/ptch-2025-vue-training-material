<template>
    <div class="task-detail">
        <!-- 模態框標題 -->
        <div class="modal-header">
            <h3>📋 任務詳情</h3>
            <button class="close-btn" @click="handleClose">✕</button>
        </div>

        <!-- 任務內容 -->
        <div class="modal-body">
            <div v-if="!isEditing" class="view-mode">
                <!-- 查看模式 -->
                <div class="task-info-grid">
                    <div class="info-item">
                        <label>任務標題：</label>
                        <span class="info-value">{{ task.title }}</span>
                    </div>

                    <div class="info-item">
                        <label>任務描述：</label>
                        <span class="info-value">{{ task.description || '無描述' }}</span>
                    </div>

                    <div class="info-item">
                        <label>優先級：</label>
                        <span class="info-value priority-badge" :class="`priority-${task.priority}`">
                            {{ getPriorityText(task.priority) }}
                        </span>
                    </div>

                    <div class="info-item">
                        <label>分類：</label>
                        <span class="info-value category-badge">{{ task.category }}</span>
                    </div>

                    <div class="info-item">
                        <label>狀態：</label>
                        <span class="info-value status-badge" :class="{ 'completed': task.completed }">
                            {{ task.completed ? '已完成' : '進行中' }}
                        </span>
                    </div>

                    <div class="info-item">
                        <label>創建時間：</label>
                        <span class="info-value">{{ formatDate(task.createdAt) }}</span>
                    </div>

                    <div v-if="task.dueDate" class="info-item">
                        <label>截止時間：</label>
                        <span class="info-value" :class="{ 'overdue': isOverdue }">
                            {{ formatDate(task.dueDate) }}
                            <span v-if="isOverdue" class="overdue-text">（已逾期）</span>
                        </span>
                    </div>
                </div>
            </div>

            <div v-else class="edit-mode">
                <!-- 編輯模式 -->
                <!-- TODO: 實現編輯表單 -->
                <form @submit.prevent="handleSave" class="edit-form">
                    <div class="form-group">
                        <label>任務標題：</label>
                        <input v-model="editData.title" type="text" class="form-control" required />
                    </div>

                    <div class="form-group">
                        <label>任務描述：</label>
                        <textarea v-model="editData.description" class="form-control" rows="3"></textarea>
                    </div>

                    <div class="form-row">
                        <div class="form-group">
                            <label>優先級：</label>
                            <select v-model="editData.priority" class="form-control">
                                <option value="low">低優先級</option>
                                <option value="medium">中優先級</option>
                                <option value="high">高優先級</option>
                            </select>
                        </div>

                        <div class="form-group">
                            <label>分類：</label>
                            <input v-model="editData.category" type="text" class="form-control" />
                        </div>
                    </div>

                    <div class="form-group">
                        <label>截止日期：</label>
                        <input v-model="editData.dueDate" type="date" class="form-control" />
                    </div>

                    <div class="form-group">
                        <label class="checkbox-label">
                            <input v-model="editData.completed" type="checkbox" class="checkbox" />
                            標記為已完成
                        </label>
                    </div>
                </form>
            </div>
        </div>

        <!-- 模態框底部 -->
        <div class="modal-footer">
            <div v-if="!isEditing" class="view-actions">
                <button class="btn btn-primary" @click="startEdit">
                    ✏️ 編輯任務
                </button>
                <button class="btn btn-secondary" @click="handleClose">
                    關閉
                </button>
            </div>

            <div v-else class="edit-actions">
                <button class="btn btn-success" @click="handleSave">
                    💾 儲存變更
                </button>
                <button class="btn btn-secondary" @click="cancelEdit">
                    ❌ 取消編輯
                </button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, reactive } from 'vue'

// TODO: 定義組件 props 和 emits
const props = defineProps({
    task: {
        type: Object,
        required: true
    }
})

const emit = defineEmits([
    'close',
    'update-task'
])

// 組件狀態
const isEditing = ref(false)
const editData = reactive({
    title: '',
    description: '',
    priority: 'medium',
    category: '',
    dueDate: '',
    completed: false
})

// 計算屬性
const isOverdue = computed(() => {
    if (!props.task.dueDate || props.task.completed) return false
    return new Date(props.task.dueDate) < new Date()
})

// TODO: 實現事件處理方法
const handleClose = () => {
    // TODO: 發射關閉事件
    emit('close')
}

const startEdit = () => {
    // TODO: 進入編輯模式，初始化編輯數據
    isEditing.value = true
    editData.title = props.task.title
    editData.description = props.task.description || ''
    editData.priority = props.task.priority
    editData.category = props.task.category
    editData.dueDate = props.task.dueDate ? formatDateForInput(props.task.dueDate) : ''
    editData.completed = props.task.completed
}

const cancelEdit = () => {
    // TODO: 取消編輯，回到查看模式
    isEditing.value = false
}

const handleSave = () => {
    // TODO: 儲存編輯的數據並發射更新事件
    const updatedTask = {
        ...props.task,
        title: editData.title.trim(),
        description: editData.description.trim(),
        priority: editData.priority,
        category: editData.category.trim(),
        dueDate: editData.dueDate ? new Date(editData.dueDate) : null,
        completed: editData.completed
    }

    emit('update-task', updatedTask)
    isEditing.value = false
}

// 工具方法
const getPriorityText = (priority) => {
    const priorityMap = {
        high: '高優先級',
        medium: '中優先級',
        low: '低優先級'
    }
    return priorityMap[priority] || '未知'
}

const formatDate = (date) => {
    if (!date) return '無'
    return new Date(date).toLocaleDateString('zh-TW', {
        year: 'numeric',
        month: 'long',
        day: 'numeric',
        hour: '2-digit',
        minute: '2-digit'
    })
}

const formatDateForInput = (date) => {
    if (!date) return ''
    return new Date(date).toISOString().split('T')[0]
}
</script>

<style scoped>
.task-detail {
    background: white;
    border-radius: 15px;
    overflow: hidden;
    box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
    max-width: 600px;
    width: 100%;
}

.modal-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 25px 30px;
    background: linear-gradient(135deg, #007bff, #0056b3);
    color: white;
}

.modal-header h3 {
    margin: 0;
    font-size: 1.4em;
    font-weight: 600;
}

.close-btn {
    background: none;
    border: none;
    color: white;
    font-size: 1.5em;
    cursor: pointer;
    padding: 5px;
    border-radius: 50%;
    transition: all 0.3s ease;
}

.close-btn:hover {
    background: rgba(255, 255, 255, 0.2);
    transform: rotate(90deg);
}

.modal-body {
    padding: 30px;
    max-height: 60vh;
    overflow-y: auto;
}

.task-info-grid {
    display: grid;
    gap: 20px;
}

.info-item {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

.info-item label {
    font-weight: 600;
    color: #495057;
    font-size: 0.9em;
}

.info-value {
    color: #333;
    font-size: 1em;
    line-height: 1.5;
}

.priority-badge {
    display: inline-block;
    padding: 6px 12px;
    border-radius: 15px;
    font-size: 0.85em;
    font-weight: 600;
}

.priority-badge.priority-high {
    background: #ffe6e6;
    color: #dc3545;
}

.priority-badge.priority-medium {
    background: #fff3cd;
    color: #856404;
}

.priority-badge.priority-low {
    background: #d4edda;
    color: #155724;
}

.category-badge {
    display: inline-block;
    padding: 6px 12px;
    background: #e7f3ff;
    color: #0066cc;
    border-radius: 15px;
    font-size: 0.85em;
    font-weight: 500;
}

.status-badge {
    display: inline-block;
    padding: 6px 12px;
    border-radius: 15px;
    font-size: 0.85em;
    font-weight: 600;
    background: #fff3cd;
    color: #856404;
}

.status-badge.completed {
    background: #d4edda;
    color: #155724;
}

.overdue {
    color: #dc3545;
}

.overdue-text {
    font-weight: 600;
}

.edit-form {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.form-group {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

.form-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 15px;
}

.form-group label {
    font-weight: 600;
    color: #495057;
    font-size: 0.9em;
}

.form-control {
    padding: 12px 15px;
    border: 2px solid #e9ecef;
    border-radius: 8px;
    font-size: 1em;
    transition: all 0.3s ease;
}

.form-control:focus {
    outline: none;
    border-color: #007bff;
    box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.1);
}

.checkbox-label {
    display: flex;
    align-items: center;
    gap: 10px;
    cursor: pointer;
    font-weight: 500;
}

.checkbox {
    width: 18px;
    height: 18px;
    accent-color: #007bff;
}

.modal-footer {
    padding: 20px 30px;
    background: #f8f9fa;
    border-top: 1px solid #e9ecef;
}

.view-actions,
.edit-actions {
    display: flex;
    gap: 12px;
    justify-content: flex-end;
}

.btn {
    padding: 10px 20px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-size: 0.9em;
    font-weight: 600;
    transition: all 0.3s ease;
}

.btn-primary {
    background: linear-gradient(135deg, #007bff, #0056b3);
    color: white;
}

.btn-primary:hover {
    background: linear-gradient(135deg, #0056b3, #004085);
    transform: translateY(-2px);
}

.btn-success {
    background: linear-gradient(135deg, #28a745, #1e7e34);
    color: white;
}

.btn-success:hover {
    background: linear-gradient(135deg, #1e7e34, #155724);
    transform: translateY(-2px);
}

.btn-secondary {
    background: #6c757d;
    color: white;
}

.btn-secondary:hover {
    background: #545b62;
    transform: translateY(-2px);
}

@media (max-width: 768px) {
    .modal-header {
        padding: 20px;
    }

    .modal-body {
        padding: 20px;
    }

    .form-row {
        grid-template-columns: 1fr;
    }

    .view-actions,
    .edit-actions {
        flex-direction: column;
    }

    .btn {
        width: 100%;
    }
}
</style>
