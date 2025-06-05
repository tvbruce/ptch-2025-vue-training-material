<template>
    <transition name="task-item" appear>
        <div class="task-item" :class="[{ completed: task.completed }, `priority-${task.priority}`]">
            <!-- 任務標題和優先級 -->
            <div class="task-header">
                <div class="task-info">
                    <h5 class="task-title" :class="{ completed: task.completed }">
                        {{ task.title }}
                    </h5>
                    <span :class="['priority-badge', task.priority]">
                        {{ priorityText }}
                    </span>
                </div>

                <div class="task-meta">
                    <span class="task-id">#{{ task.id }}</span>
                    <span class="task-date" :title="formatFullDate(task.createdAt)">
                        {{ formatRelativeDate(task.createdAt) }}
                    </span>
                </div>
            </div>

            <!-- 任務描述 -->
            <p v-if="task.description" class="task-description" :class="{ completed: task.completed }">
                {{ task.description }}
            </p>

            <!-- 進度條（如果有子任務） -->
            <div v-if="task.subtasks && task.subtasks.length > 0" class="progress-section">
                <div class="progress-info">
                    <span>進度：{{ completedSubtasks }} / {{ task.subtasks.length }}</span>
                    <span class="progress-percentage">{{ progressPercentage }}%</span>
                </div>
                <div class="progress-bar">
                    <div class="progress-fill" :style="{ width: `${progressPercentage}%` }"></div>
                </div>
            </div>

            <!-- 標籤 -->
            <div v-if="task.tags && task.tags.length > 0" class="task-tags">
                <span v-for="tag in task.tags" :key="tag" class="tag">
                    {{ tag }}
                </span>
            </div>

            <!-- 操作按鈕 -->
            <div class="task-actions">
                <button @click="handleToggleComplete" :class="['btn', 'btn-toggle', { completed: task.completed }]"
                    :title="task.completed ? '標記為未完成' : '標記為已完成'">
                    <span class="icon">{{ task.completed ? '↩️' : '✅' }}</span>
                    {{ task.completed ? '未完成' : '完成' }}
                </button>

                <button @click="handleEdit" class="btn btn-edit" title="編輯任務">
                    <span class="icon">✏️</span>
                    編輯
                </button>

                <button @click="handleDelete" class="btn btn-danger" title="刪除任務">
                    <span class="icon">🗑️</span>
                    刪除
                </button>
            </div>

            <!-- 完成動畫效果 -->
            <div v-if="showCompletionEffect" class="completion-effect">
                <span class="celebration">🎉</span>
            </div>
        </div>
    </transition>
</template>

<script setup>
import { computed, ref } from 'vue'

// 定義 props
const props = defineProps({
    task: {
        type: Object,
        required: true,
        validator: (task) => {
            return task && typeof task === 'object' && task.id && task.title
        }
    }
})

// 定義 emit 事件
const emit = defineEmits(['toggle-complete', 'delete-task', 'edit-task'])

// 完成效果狀態
const showCompletionEffect = ref(false)

// 計算屬性
const priorityText = computed(() => {
    const priorityMap = {
        high: '高',
        medium: '中',
        low: '低'
    }
    return priorityMap[props.task.priority] || '未知'
})

const completedSubtasks = computed(() => {
    if (!props.task.subtasks) return 0
    return props.task.subtasks.filter(subtask => subtask.completed).length
})

const progressPercentage = computed(() => {
    if (!props.task.subtasks || props.task.subtasks.length === 0) return 0
    return Math.round((completedSubtasks.value / props.task.subtasks.length) * 100)
})

// 日期格式化
const formatRelativeDate = (date) => {
    if (!date) return ''

    const now = new Date()
    const taskDate = new Date(date)
    const diffInHours = Math.floor((now - taskDate) / (1000 * 60 * 60))

    if (diffInHours < 1) return '剛才'
    if (diffInHours < 24) return `${diffInHours} 小時前`

    const diffInDays = Math.floor(diffInHours / 24)
    if (diffInDays < 7) return `${diffInDays} 天前`

    return taskDate.toLocaleDateString('zh-TW')
}

const formatFullDate = (date) => {
    if (!date) return ''
    return new Date(date).toLocaleString('zh-TW')
}

// 事件處理
const handleToggleComplete = () => {
    // 如果要標記為完成，顯示慶祝效果
    if (!props.task.completed) {
        showCompletionEffect.value = true
        setTimeout(() => {
            showCompletionEffect.value = false
        }, 1500)
    }

    emit('toggle-complete', props.task.id)
}

const handleDelete = () => {
    if (confirm(`確定要刪除任務「${props.task.title}」嗎？`)) {
        emit('delete-task', props.task.id)
    }
}

const handleEdit = () => {
    emit('edit-task', props.task.id)
}
</script>

<style scoped>
/* 動畫效果 */
.task-item-enter-active,
.task-item-leave-active {
    transition: all 0.3s ease;
}

.task-item-enter-from {
    opacity: 0;
    transform: translateY(-20px);
}

.task-item-leave-to {
    opacity: 0;
    transform: translateX(100%);
}

.task-item {
    position: relative;
    background: white;
    border: 2px solid #e9ecef;
    border-radius: 12px;
    padding: 1.5rem;
    margin-bottom: 1rem;
    transition: all 0.3s ease;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    overflow: hidden;
}

.task-item:hover {
    border-color: #20c997;
    transform: translateY(-2px);
    box-shadow: 0 4px 16px rgba(32, 201, 151, 0.2);
}

.task-item.completed {
    background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
    border-color: #ced4da;
}

/* 優先級樣式 */
.task-item.priority-high {
    border-left: 4px solid #dc3545;
}

.task-item.priority-medium {
    border-left: 4px solid #ffc107;
}

.task-item.priority-low {
    border-left: 4px solid #28a745;
}

.task-header {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    margin-bottom: 1rem;
    gap: 1rem;
}

.task-info {
    flex: 1;
    display: flex;
    align-items: flex-start;
    gap: 1rem;
}

.task-title {
    margin: 0;
    color: #495057;
    font-size: 1.1rem;
    font-weight: 600;
    flex: 1;
    line-height: 1.4;
}

.task-title.completed {
    text-decoration: line-through;
    color: #6c757d;
}

.priority-badge {
    padding: 0.25rem 0.75rem;
    border-radius: 20px;
    font-size: 0.75rem;
    font-weight: bold;
    text-transform: uppercase;
    white-space: nowrap;
}

.priority-badge.high {
    background: #f8d7da;
    color: #721c24;
    border: 1px solid #f5c6cb;
}

.priority-badge.medium {
    background: #fff3cd;
    color: #856404;
    border: 1px solid #ffeeba;
}

.priority-badge.low {
    background: #d4edda;
    color: #155724;
    border: 1px solid #c3e6cb;
}

.task-meta {
    display: flex;
    flex-direction: column;
    align-items: flex-end;
    gap: 0.25rem;
    font-size: 0.8rem;
    color: #6c757d;
}

.task-id {
    font-family: monospace;
    background: #e9ecef;
    padding: 0.2rem 0.4rem;
    border-radius: 4px;
}

.task-description {
    color: #6c757d;
    margin: 0 0 1rem 0;
    line-height: 1.6;
    font-size: 0.95rem;
}

.task-description.completed {
    text-decoration: line-through;
    color: #adb5bd;
}

.progress-section {
    margin: 1rem 0;
    padding: 1rem;
    background: #f8f9fa;
    border-radius: 8px;
}

.progress-info {
    display: flex;
    justify-content: space-between;
    margin-bottom: 0.5rem;
    font-size: 0.875rem;
    color: #495057;
}

.progress-percentage {
    font-weight: bold;
    color: #20c997;
}

.progress-bar {
    width: 100%;
    height: 8px;
    background: #dee2e6;
    border-radius: 4px;
    overflow: hidden;
}

.progress-fill {
    height: 100%;
    background: linear-gradient(90deg, #20c997, #1bae87);
    transition: width 0.3s ease;
}

.task-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
    margin: 1rem 0;
}

.tag {
    background: #e7f3ff;
    color: #0056b3;
    padding: 0.25rem 0.5rem;
    border-radius: 12px;
    font-size: 0.75rem;
    border: 1px solid #b3d4fc;
}

.task-actions {
    display: flex;
    gap: 0.5rem;
    margin-top: 1rem;
}

.btn {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.5rem 1rem;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-size: 0.875rem;
    font-weight: 500;
    transition: all 0.3s ease;
    text-decoration: none;
}

.btn .icon {
    font-size: 1rem;
}

.btn-toggle {
    background: #28a745;
    color: white;
    flex: 1;
}

.btn-toggle:hover {
    background: #218838;
    transform: translateY(-1px);
}

.btn-toggle.completed {
    background: #6c757d;
}

.btn-toggle.completed:hover {
    background: #545b62;
}

.btn-edit {
    background: #007bff;
    color: white;
}

.btn-edit:hover {
    background: #0056b3;
    transform: translateY(-1px);
}

.btn-danger {
    background: #dc3545;
    color: white;
}

.btn-danger:hover {
    background: #c82333;
    transform: translateY(-1px);
}

/* 完成慶祝效果 */
.completion-effect {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    font-size: 3rem;
    animation: celebrate 1.5s ease-out forwards;
    pointer-events: none;
    z-index: 10;
}

@keyframes celebrate {
    0% {
        transform: translate(-50%, -50%) scale(0) rotate(0deg);
        opacity: 1;
    }

    50% {
        transform: translate(-50%, -50%) scale(1.2) rotate(180deg);
        opacity: 1;
    }

    100% {
        transform: translate(-50%, -50%) scale(0) rotate(360deg);
        opacity: 0;
    }
}

@media (max-width: 768px) {
    .task-header {
        flex-direction: column;
        gap: 0.5rem;
    }

    .task-info {
        flex-direction: column;
        gap: 0.5rem;
    }

    .task-meta {
        flex-direction: row;
        align-items: center;
        gap: 1rem;
    }

    .task-actions {
        flex-direction: column;
    }

    .btn {
        justify-content: center;
    }
}
</style>
