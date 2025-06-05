<template>
    <div class="task-item" :class="{ 'completed': task.completed, [`priority-${task.priority}`]: true }">
        <div class="task-checkbox">
            <input type="checkbox" :checked="task.completed" @change="$emit('toggle-complete', task.id)"
                :id="`task-${task.id}`">
            <label :for="`task-${task.id}`" class="checkbox-label"></label>
        </div>

        <div class="task-content">
            <div class="task-header">
                <h5 class="task-title" :class="{ 'completed': task.completed }">
                    {{ task.title }}
                </h5>
                <div class="task-meta">
                    <span class="priority-badge" :class="`priority-${task.priority}`">
                        {{ getPriorityLabel(task.priority) }}
                    </span>
                    <span v-if="task.dueDate" class="due-date" :class="{ 'overdue': isOverdue }">
                        {{ formatDate(task.dueDate) }}
                    </span>
                </div>
            </div>

            <p v-if="task.description" class="task-description">
                {{ task.description }}
            </p>

            <div class="task-footer">
                <span class="created-date">
                    建立於 {{ formatDate(task.createdAt) }}
                </span>
            </div>
        </div>

        <div class="task-actions">
            <button @click="$emit('edit-task', task)" class="action-btn edit-btn" title="編輯任務">
                ✏️
            </button>
            <button @click="$emit('delete-task', task.id)" class="action-btn delete-btn" title="刪除任務">
                🗑️
            </button>
        </div>
    </div>
</template>

<script setup>
import { computed } from 'vue'

// 定義 props
const props = defineProps({
    task: {
        type: Object,
        required: true
    }
})

// 定義事件
defineEmits(['toggle-complete', 'delete-task', 'edit-task'])

// 計算是否過期
const isOverdue = computed(() => {
    if (!props.task.dueDate || props.task.completed) return false
    return new Date(props.task.dueDate) < new Date()
})

// 格式化日期
const formatDate = (date) => {
    if (!date) return ''
    return new Date(date).toLocaleDateString('zh-TW', {
        year: 'numeric',
        month: 'short',
        day: 'numeric'
    })
}

// 獲取優先級標籤
const getPriorityLabel = (priority) => {
    const labels = {
        'low': '低',
        'medium': '中',
        'high': '高'
    }
    return labels[priority] || priority
}
</script>

<style scoped>
.task-item {
    display: flex;
    align-items: flex-start;
    gap: 15px;
    padding: 20px;
    margin-bottom: 15px;
    background: white;
    border-radius: 12px;
    border: 2px solid #e1e5e9;
    transition: all 0.3s ease;
    position: relative;
}

.task-item:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
}

.task-item.completed {
    opacity: 0.7;
    background: #f8f9fa;
}

.task-item.priority-high {
    border-left: 6px solid #e74c3c;
}

.task-item.priority-medium {
    border-left: 6px solid #f39c12;
}

.task-item.priority-low {
    border-left: 6px solid #27ae60;
}

.task-checkbox {
    position: relative;
    margin-top: 2px;
}

.task-checkbox input[type="checkbox"] {
    opacity: 0;
    position: absolute;
    width: 20px;
    height: 20px;
    cursor: pointer;
}

.checkbox-label {
    display: block;
    width: 20px;
    height: 20px;
    border: 2px solid #bdc3c7;
    border-radius: 4px;
    cursor: pointer;
    transition: all 0.3s ease;
    position: relative;
}

.checkbox-label::after {
    content: '✓';
    position: absolute;
    top: -2px;
    left: 2px;
    color: white;
    font-size: 14px;
    font-weight: bold;
    opacity: 0;
    transition: opacity 0.3s ease;
}

.task-checkbox input[type="checkbox"]:checked+.checkbox-label {
    background: #27ae60;
    border-color: #27ae60;
}

.task-checkbox input[type="checkbox"]:checked+.checkbox-label::after {
    opacity: 1;
}

.task-content {
    flex: 1;
    min-width: 0;
}

.task-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-bottom: 8px;
    gap: 15px;
}

.task-title {
    margin: 0;
    color: #2c3e50;
    font-size: 1.1rem;
    font-weight: 600;
    line-height: 1.3;
    word-break: break-word;
}

.task-title.completed {
    text-decoration: line-through;
    color: #7f8c8d;
}

.task-meta {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    gap: 5px;
    flex-shrink: 0;
}

.priority-badge {
    padding: 4px 8px;
    border-radius: 12px;
    font-size: 0.75rem;
    font-weight: 600;
    text-transform: uppercase;
}

.priority-badge.priority-high {
    background: #ffebee;
    color: #c62828;
}

.priority-badge.priority-medium {
    background: #fff3e0;
    color: #ef6c00;
}

.priority-badge.priority-low {
    background: #e8f5e8;
    color: #2e7d32;
}

.due-date {
    font-size: 0.8rem;
    color: #7f8c8d;
    padding: 2px 6px;
    border-radius: 8px;
    background: #f8f9fa;
}

.due-date.overdue {
    background: #ffebee;
    color: #c62828;
    font-weight: 600;
}

.task-description {
    margin: 0 0 10px 0;
    color: #5a6c7d;
    font-size: 0.9rem;
    line-height: 1.4;
    word-break: break-word;
}

.task-footer {
    margin-top: 10px;
}

.created-date {
    font-size: 0.75rem;
    color: #95a5a6;
    font-style: italic;
}

.task-actions {
    display: flex;
    flex-direction: column;
    gap: 8px;
    flex-shrink: 0;
}

.action-btn {
    width: 36px;
    height: 36px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 14px;
}

.edit-btn {
    background: #e3f2fd;
    color: #1976d2;
}

.edit-btn:hover {
    background: #bbdefb;
    transform: scale(1.1);
}

.delete-btn {
    background: #ffebee;
    color: #c62828;
}

.delete-btn:hover {
    background: #ffcdd2;
    transform: scale(1.1);
}

@media (max-width: 768px) {
    .task-item {
        flex-direction: column;
        gap: 10px;
    }

    .task-header {
        flex-direction: column;
        align-items: flex-start;
        gap: 8px;
    }

    .task-meta {
        flex-direction: row;
        align-items: center;
    }

    .task-actions {
        flex-direction: row;
        justify-content: flex-end;
    }
}
</style>
