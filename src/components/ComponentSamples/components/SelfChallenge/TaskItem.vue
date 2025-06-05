<template>
  <div class="task-item" :class="{ 'completed': task.completed, [`priority-${task.priority}`]: true }">
    <div class="task-content">
      <!-- 完成狀態切換 -->
      <div class="task-checkbox">
        <!-- TODO: 實現完成狀態切換 -->
        <!-- 提示：使用 @click 事件發射 toggle-complete -->
        <input type="checkbox" :checked="task.completed" @change="" class="checkbox" />
      </div>

      <!-- 任務資訊 -->
      <div class="task-info">
        <h4 class="task-title" :class="{ 'completed-text': task.completed }">
          {{ task.title }}
        </h4>
        <p class="task-description">{{ task.description }}</p>

        <!-- 任務標籤 -->
        <div class="task-tags">
          <span class="tag priority-tag" :class="`priority-${task.priority}`">
            {{ /* TODO: 顯示優先級文字 */ }}
          </span>
          <span class="tag category-tag">{{ task.category }}</span>
          <span class="tag date-tag">{{ /* TODO: 格式化顯示日期 */ }}</span>
        </div>
      </div>

      <!-- 操作按鈕區域 -->
      <div class="task-actions">
        <!-- TODO: 使用具名插槽允許父組件自定義操作按鈕 -->
        <!-- 提示：<slot name="actions"> -->

        <!-- 預設操作按鈕 -->
        <button class="btn btn-sm btn-edit" @click="" :disabled="task.completed">
          編輯
        </button>


        <button class="btn btn-sm btn-delete" @click="">
          刪除
        </button>
      </div>
    </div>

    <!-- 任務進度條（根據優先級顯示） -->
    <div class="task-progress" v-if="!task.completed">
      <div class="progress-bar" :class="`priority-${task.priority}`"></div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

// TODO: 定義組件接收的 props
// 提示：使用 defineProps 定義 task 屬性
const props = defineProps({
  // TODO: 定義 task prop，類型為 Object，必需
})

// TODO: 定義組件發出的事件
// 提示：使用 defineEmits 定義各種事件
const emit = defineEmits([
  // TODO: 定義事件名稱
  // 提示：'toggle-complete', 'delete-task', 'edit-task'
])

// 計算屬性
const priorityText = computed(() => {
  // TODO: 根據 task.priority 返回對應的中文文字
  return '未知'
})

// TODO: 實現事件處理方法
const handleToggleComplete = () => {
  // TODO: 發射切換完成狀態事件
  // 提示：emit('toggle-complete', props.task.id)
}

const handleDelete = () => {
  // TODO: 發射刪除任務事件
  // 提示：可以加上確認對話框
}

const handleEdit = () => {
  // TODO: 發射編輯任務事件
  // 提示：可以傳遞任務 ID 或整個任務對象
}

// 工具方法
const formatDate = (date) => {
  // TODO: 格式化日期顯示
  if (!date) return '無期限'
  // 提示：使用 new Date(date).toLocaleDateString('zh-TW')
  return '日期'
}
</script>

<style scoped>
.task-item {
  background: white;
  border: 2px solid #e9ecef;
  border-radius: 12px;
  padding: 20px;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.task-item:hover {
  border-color: #007bff;
  box-shadow: 0 4px 15px rgba(0, 123, 255, 0.1);
  transform: translateY(-2px);
}

.task-item.completed {
  background: #f8f9fa;
  border-color: #28a745;
  opacity: 0.8;
}

.task-item.priority-high {
  border-left: 5px solid #dc3545;
}

.task-item.priority-medium {
  border-left: 5px solid #ffc107;
}

.task-item.priority-low {
  border-left: 5px solid #28a745;
}

.task-content {
  display: flex;
  align-items: flex-start;
  gap: 15px;
}

.task-checkbox {
  flex-shrink: 0;
  margin-top: 5px;
}

.checkbox {
  width: 20px;
  height: 20px;
  cursor: pointer;
  accent-color: #007bff;
}

.task-info {
  flex: 1;
  min-width: 0;
}

.task-title {
  margin: 0 0 8px 0;
  font-size: 1.2em;
  font-weight: 600;
  color: #333;
  transition: all 0.3s ease;
}

.task-title.completed-text {
  text-decoration: line-through;
  color: #6c757d;
}

.task-description {
  margin: 0 0 12px 0;
  color: #666;
  line-height: 1.5;
  font-size: 0.95em;
}

.task-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
}

.tag {
  padding: 4px 8px;
  border-radius: 12px;
  font-size: 0.8em;
  font-weight: 500;
}

.priority-tag.priority-high {
  background: #ffe6e6;
  color: #dc3545;
}

.priority-tag.priority-medium {
  background: #fff3cd;
  color: #856404;
}

.priority-tag.priority-low {
  background: #d4edda;
  color: #155724;
}

.category-tag {
  background: #e7f3ff;
  color: #0066cc;
}

.date-tag {
  background: #f8f9fa;
  color: #6c757d;
}

.task-actions {
  display: flex;
  flex-direction: column;
  gap: 8px;
  flex-shrink: 0;
}

.task-progress {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: #e9ecef;
}

.progress-bar {
  height: 100%;
  width: 100%;
  animation: pulse 2s infinite;
}

.progress-bar.priority-high {
  background: linear-gradient(90deg, #dc3545, #ff6b7a);
}

.progress-bar.priority-medium {
  background: linear-gradient(90deg, #ffc107, #ffda6a);
}

.progress-bar.priority-low {
  background: linear-gradient(90deg, #28a745, #6bcf7f);
}

.btn {
  padding: 6px 12px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-size: 0.85em;
  font-weight: 500;
  transition: all 0.3s ease;
  text-align: center;
}

.btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}

.btn-sm {
  padding: 4px 8px;
  font-size: 0.8em;
}

.btn-edit {
  background: #17a2b8;
  color: white;
}

.btn-edit:hover:not(:disabled) {
  background: #138496;
  transform: translateY(-1px);
}

.btn-delete {
  background: #dc3545;
  color: white;
}

.btn-delete:hover {
  background: #c82333;
  transform: translateY(-1px);
}

@keyframes pulse {

  0%,
  100% {
    opacity: 0.7;
  }

  50% {
    opacity: 1;
  }
}

@media (max-width: 768px) {
  .task-content {
    flex-direction: column;
    gap: 10px;
  }

  .task-actions {
    flex-direction: row;
    justify-content: flex-end;
  }

  .task-tags {
    gap: 6px;
  }

  .tag {
    font-size: 0.75em;
  }
}
</style>
