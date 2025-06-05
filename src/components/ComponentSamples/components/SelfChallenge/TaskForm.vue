<template>
  <div class="task-form">
    <h4>📝 新增任務</h4>

    <form @submit.prevent="handleSubmit" class="form">
      <!-- 任務標題 -->
      <div class="form-group">
        <label for="title">任務標題 *</label>
        <input id="title" type="text" class="form-control" placeholder="請輸入任務標題" required v-model="formData.title" />
      </div>

      <!-- 任務描述 -->
      <div class="form-group">
        <label for="description">任務描述</label>
        <textarea id="description" class="form-control" placeholder="請輸入任務描述" rows="3"
          v-model="formData.description"></textarea>
      </div>

      <!-- 優先級和分類 -->
      <div class="form-row">
        <div class="form-group">
          <label for="priority">優先級</label>
          <select id="priority" class="form-control" v-model="formData.priority">
            <option value="low">低優先級</option>
            <option value="medium">中優先級</option>
            <option value="high">高優先級</option>
          </select>
        </div>

        <div class="form-group">
          <label for="category">分類</label>
          <input id="category" type="text" class="form-control" placeholder="例如：工作、學習" v-model="formData.category" />
        </div>
      </div>

      <!-- 截止日期 -->
      <div class="form-group">
        <label for="dueDate">截止日期</label>
        <input id="dueDate" type="date" class="form-control" v-model="formData.dueDate" />
      </div>

      <!-- 提交按鈕 -->
      <div class="form-actions">
        <button type="submit" class="btn btn-primary">
          ✅ 新增任務
        </button>

        <button type="button" class="btn btn-secondary" @click="resetForm">
          🔄 重置
        </button>
      </div>
    </form>

    <!-- 表單預覽 -->
    <div class="form-preview">
      <h5>📋 任務預覽</h5>
      <div class="preview-content">
        <p><strong>標題：</strong>{{ formData.title }}</p>
        <p><strong>描述：</strong>{{ formData.description }}</p>
        <p><strong>優先級：</strong>{{ priorityText }}</p>
        <p><strong>分類：</strong>{{ formData.category }}</p>
        <p><strong>截止日期：</strong>{{ formatDate(formData.dueDate) }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, reactive } from 'vue'

// 🎯 任務：定義 emit 事件
// 提示：const emit = defineEmits(['add-task'])
const emit = defineEmits(['add-task'])

// TODO: 定義表單數據
// 提示：使用 reactive 創建表單對象
const formData = reactive({
  title: '',
  description: '',
  priority: 'medium',
  category: '',
  dueDate: ''
})

// TODO: 定義表單狀態
const isSubmitting = ref(false)
const errors = reactive({
  // TODO: 定義錯誤訊息字段
})

// TODO: 實現計算屬性
const today = computed(() => {
  // TODO: 返回今天的日期字符串，格式 YYYY-MM-DD
  return ''
})

const priorityText = computed(() => {
  // TODO: 根據優先級返回中文文字
  return ''
})

const isFormValid = computed(() => {
  // TODO: 實現表單驗證邏輯
  return false
})

// 🎯 任務：實作表單提交處理
const handleSubmit = () => {
  // 請在這裡實作表單提交邏輯
  // 1. 驗證表單資料
  // 2. 發送 add-task 事件給父組件
  // 3. 重置表單

  // 基本驗證
  if (!formData.title.trim()) {
    alert('請輸入任務標題')
    return
  }

  // 發送事件給父組件
  emit('add-task', {
    title: formData.title.trim(),
    description: formData.description.trim(),
    priority: formData.priority,
    category: formData.category.trim(),
    dueDate: formData.dueDate,
    completed: false,
    createdAt: new Date()
  })

  // 重置表單
  resetForm()
}

// 🎯 任務：實作重置表單
const resetForm = () => {
  // 請在這裡實作重置表單邏輯
  formData.title = ''
  formData.description = ''
  formData.priority = 'medium'
  formData.category = ''
  formData.dueDate = ''
}

// 工具方法
const formatDate = (dateString) => {
  // TODO: 格式化日期顯示
  if (!dateString) return ''
  return ''
}
</script>

<style scoped>
.task-form {
  background: white;
  border-radius: 12px;
  padding: 25px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.task-form h4 {
  margin: 0 0 20px 0;
  color: #333;
  font-size: 1.3em;
  text-align: center;
}

.form {
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
  color: #555;
  font-size: 0.95em;
}

.form-control {
  padding: 12px 15px;
  border: 2px solid #e9ecef;
  border-radius: 8px;
  font-size: 1em;
  transition: all 0.3s ease;
  background: white;
}

.form-control:focus {
  outline: none;
  border-color: #007bff;
  box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.1);
}

.form-control.error {
  border-color: #dc3545;
}

.form-control.error:focus {
  box-shadow: 0 0 0 3px rgba(220, 53, 69, 0.1);
}

.error-message {
  color: #dc3545;
  font-size: 0.85em;
  margin-top: 4px;
}

.form-actions {
  display: flex;
  gap: 12px;
  justify-content: center;
  margin-top: 10px;
}

.btn {
  padding: 12px 24px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 1em;
  font-weight: 600;
  transition: all 0.3s ease;
  min-width: 120px;
}

.btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.btn-primary {
  background: linear-gradient(135deg, #007bff, #0056b3);
  color: white;
}

.btn-primary:hover:not(:disabled) {
  background: linear-gradient(135deg, #0056b3, #004085);
  transform: translateY(-2px);
  box-shadow: 0 4px 15px rgba(0, 123, 255, 0.3);
}

.btn-secondary {
  background: #6c757d;
  color: white;
}

.btn-secondary:hover {
  background: #545b62;
  transform: translateY(-2px);
}

.form-preview {
  margin-top: 25px;
  padding: 20px;
  background: #f8f9fa;
  border-radius: 10px;
  border-left: 4px solid #007bff;
}

.form-preview h5 {
  margin: 0 0 15px 0;
  color: #333;
  font-size: 1.1em;
}

.preview-content {
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.preview-content p {
  margin: 0;
  color: #555;
  font-size: 0.95em;
}

.preview-content strong {
  color: #333;
}

@media (max-width: 768px) {
  .task-form {
    padding: 20px;
  }

  .form-row {
    grid-template-columns: 1fr;
    gap: 20px;
  }

  .form-actions {
    flex-direction: column;
  }

  .btn {
    width: 100%;
  }
}
</style>
