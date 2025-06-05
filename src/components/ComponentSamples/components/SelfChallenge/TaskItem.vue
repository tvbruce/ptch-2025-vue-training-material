<template>
  <div class="task-item" :class="{ completed: task.completed }">
    <div class="task-header">
      <h5 class="task-title">{{ task.title }}</h5>
      <span :class="['priority-badge', task.priority]">
        {{ priorityText }}
      </span>
    </div>

    <p class="task-description">{{ task.description }}</p>

    <div class="task-meta">
      <span class="task-date">
        建立於：{{ formatDate(task.createdAt) }}
      </span>
      <span v-if="task.dueDate" class="task-due">
        截止：{{ formatDate(task.dueDate) }}
      </span>
    </div>

    <div class="task-actions">
      <!-- 🎯 任務：實作切換完成狀態按鈕 -->
      <button @click="handleToggleComplete" :class="['btn', 'btn-toggle', { completed: task.completed }]">
        {{ task.completed ? '✅ 已完成' : '⭕ 標記完成' }}
      </button>

      <!-- 🎯 任務：實作刪除按鈕 -->
      <button @click="handleDelete" class="btn btn-danger">
        🗑️ 刪除
      </button>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

// 🎯 任務：定義 props
// 提示：const props = defineProps(['task'])
const props = defineProps({
  task: {
    type: Object,
    required: true
  }
})

// 🎯 任務：定義 emit 事件
// 提示：const emit = defineEmits(['toggle-complete', 'delete-task'])
const emit = defineEmits(['toggle-complete', 'delete-task'])

// 優先級文字
const priorityText = computed(() => {
  const priorityMap = {
    high: '高優先級',
    medium: '中優先級',
    low: '低優先級'
  }
  return priorityMap[props.task.priority] || '未知'
})

// 🎯 任務：實作切換完成狀態處理
const handleToggleComplete = () => {
  // 請在這裡實作切換完成狀態邏輯
  // 發送 toggle-complete 事件給父組件
  emit('toggle-complete', props.task.id)
}

// 🎯 任務：實作刪除處理
const handleDelete = () => {
  // 請在這裡實作刪除邏輯
  // 可以加入確認對話框
  if (confirm(`確定要刪除任務「${props.task.title}」嗎？`)) {
    emit('delete-task', props.task.id)
  }
}

// 日期格式化
const formatDate = (date) => {
  if (!date) return ''
  return new Date(date).toLocaleDateString('zh-TW')
}
</script>

<style scoped>
.task-item {
  background: white;
  border: 2px solid #e9ecef;
  border-radius: 8px;
  padding: 1.5rem;
  transition: all 0.3s ease;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.task-item:hover {
  border-color: #20c997;
  transform: translateY(-2px);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
}

.task-item.completed {
  opacity: 0.7;
  background: #f8f9fa;
}

.task-header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  margin-bottom: 1rem;
}

.task-title {
  margin: 0;
  color: #495057;
  font-size: 1.1rem;
  flex: 1;
}

.task-item.completed .task-title {
  text-decoration: line-through;
  color: #6c757d;
}

.priority-badge {
  padding: 0.25rem 0.5rem;
  border-radius: 12px;
  font-size: 0.8rem;
  font-weight: bold;
  text-transform: uppercase;
}

.priority-badge.high {
  background: #f8d7da;
  color: #721c24;
}

.priority-badge.medium {
  background: #fff3cd;
  color: #856404;
}

.priority-badge.low {
  background: #d4edda;
  color: #155724;
}

.task-description {
  color: #6c757d;
  margin: 0 0 1rem 0;
  line-height: 1.5;
}

.task-item.completed .task-description {
  text-decoration: line-through;
}

.task-meta {
  display: flex;
  gap: 1rem;
  margin-bottom: 1rem;
  font-size: 0.9rem;
  color: #6c757d;
}

.task-actions {
  display: flex;
  gap: 0.5rem;
}

.btn {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9rem;
  transition: all 0.3s ease;
}

.btn-toggle {
  background: #28a745;
  color: white;
  flex: 1;
}

.btn-toggle.completed {
  background: #6c757d;
}

.btn-danger {
  background: #dc3545;
  color: white;
}

.btn:hover {
  opacity: 0.9;
  transform: translateY(-1px);
}

@media (max-width: 768px) {
  .task-header {
    flex-direction: column;
    gap: 0.5rem;
  }

  .task-meta {
    flex-direction: column;
    gap: 0.25rem;
  }

  .task-actions {
    flex-direction: column;
  }
}
</style>
