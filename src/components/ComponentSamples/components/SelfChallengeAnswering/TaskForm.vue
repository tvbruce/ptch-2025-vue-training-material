<template>
  <div class="task-form">
    <h4>📝 新增任務表單</h4>

    <form @submit.prevent="handleSubmit" class="form">
      <!-- 🎯 任務：建立任務標題輸入欄位 -->
      <div class="form-group">
        <label for="title">任務標題 *</label>
        <input id="title" type="text" class="form-input" placeholder="請輸入任務標題" required />
      </div>

      <!-- 🎯 任務：建立任務描述輸入欄位 -->
      <div class="form-group">
        <label for="description">任務描述</label>
        <textarea id="description" class="form-input" placeholder="請輸入任務描述" rows="3"></textarea>
      </div>

      <!-- 🎯 任務：建立優先級選擇欄位 -->
      <div class="form-group">
        <label for="priority">優先級</label>
        <select id="priority" class="form-input">
          <option value="low">低優先級</option>
          <option value="medium">中優先級</option>
          <option value="high">高優先級</option>
        </select>
      </div>

      <!-- 🎯 任務：建立表單按鈕 -->
      <div class="form-actions">
        <button type="submit" class="btn btn-primary">
          新增任務
        </button>
        <button type="button" @click="resetForm" class="btn btn-secondary">
          重置
        </button>
      </div>
    </form>
  </div>
</template>

<script setup>
// 🎯 任務：導入需要的 Vue 函數
// 提示：import { ref } from 'vue'

// 🎯 任務：定義 emit 事件
// 提示：const emit = defineEmits(['add-task'])

// 🎯 任務：建立表單資料
// 提示：使用 ref 創建響應式資料
// const formData = ref({
//   title: '',
//   description: '',
//   priority: 'medium'
// })

// 🎯 任務：實作表單提交處理
const handleSubmit = () => {
  // 請在這裡實作表單提交邏輯
  // 1. 驗證表單資料（檢查 title 是否為空）
  // 2. 發送 add-task 事件給父組件，傳遞表單資料
  // 3. 重置表單
  console.log('🎯 待實作：表單提交功能')
}

// 🎯 任務：實作重置表單
const resetForm = () => {
  // 請在這裡實作重置表單邏輯
  // 將 formData 的所有屬性重置為初始值
  console.log('🎯 待實作：重置表單功能')
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
  margin: 0 0 1rem 0;
  color: #495057;
}

.form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
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
  transition: border-color 0.3s ease;
}

.form-input:focus {
  outline: none;
  border-color: #20c997;
}

.form-actions {
  display: flex;
  gap: 1rem;
  margin-top: 1rem;
}

.btn {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 1rem;
  transition: background-color 0.3s ease;
}

.btn-primary {
  background: #007bff;
  color: white;
}

.btn-secondary {
  background: #6c757d;
  color: white;
}

.btn:hover {
  opacity: 0.9;
}

@media (max-width: 768px) {
  .form-actions {
    flex-direction: column;
  }
}
</style>
