<template>
  <div class="article-editor">
    <div class="editor-header">
      <h4>✍️ 創建新文章</h4>
      <p>填寫文章信息並發布</p>
    </div>

    <form @submit.prevent="createArticle" class="editor-form">
      <div class="form-group">
        <label for="title">文章標題 *</label>
        <input id="title" v-model="articleForm.title" type="text" placeholder="請輸入文章標題" required class="form-input" />
      </div>

      <div class="form-group">
        <label for="author">作者 *</label>
        <input id="author" v-model="articleForm.author" type="text" placeholder="請輸入作者姓名" required class="form-input" />
      </div>

      <div class="form-group">
        <label for="content">文章內容 *</label>
        <textarea id="content" v-model="articleForm.content" placeholder="請輸入文章內容" required class="form-textarea"
          rows="6"></textarea>
      </div>

      <div class="form-actions">
        <button type="submit" class="submit-btn" :disabled="!isFormValid">
          📝 發布文章
        </button>
        <button type="button" @click="resetForm" class="reset-btn">
          🔄 重置表單
        </button>
      </div>
    </form>

    <div class="editor-info">
      <div class="info-item">
        <span class="info-label">字數統計:</span>
        <span class="info-value">{{ contentLength }} 字</span>
      </div>
      <div class="info-item">
        <span class="info-label">表單狀態:</span>
        <span class="info-value" :class="{ valid: isFormValid, invalid: !isFormValid }">
          {{ isFormValid ? '✅ 有效' : '❌ 無效' }}
        </span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

// 定義事件發射
const emit = defineEmits(['article-created', 'task-completed'])

// 表單數據
const articleForm = ref({
  title: '',
  author: '',
  content: ''
})

// 計算屬性
const contentLength = computed(() => {
  return articleForm.value.content.length
})

const isFormValid = computed(() => {
  return articleForm.value.title.trim() !== '' &&
    articleForm.value.author.trim() !== '' &&
    articleForm.value.content.trim() !== ''
})

// 創建文章方法
const createArticle = () => {
  if (!isFormValid.value) return

  const newArticle = {
    title: articleForm.value.title.trim(),
    author: articleForm.value.author.trim(),
    content: articleForm.value.content.trim()
  }

  // 發射事件到父組件
  emit('article-created', newArticle)
  emit('task-completed', 'eventEmit')

  // 重置表單
  resetForm()

  // 顯示成功消息
  alert('文章發布成功！')
}

// 重置表單方法
const resetForm = () => {
  articleForm.value = {
    title: '',
    author: '',
    content: ''
  }
}

// 組件掛載時標記props任務完成
onMounted(() => {
  emit('task-completed', 'propsUsage')
})
</script>

<style scoped>
.article-editor {
  background: #f8f9fa;
  padding: 25px;
  border-radius: 12px;
  border: 2px solid #e9ecef;
}

.editor-header {
  text-align: center;
  margin-bottom: 25px;
}

.editor-header h4 {
  margin: 0 0 8px 0;
  color: #495057;
  font-size: 1.3em;
}

.editor-header p {
  margin: 0;
  color: #6c757d;
  font-size: 0.9em;
}

.editor-form {
  margin-bottom: 20px;
}

.form-group {
  margin-bottom: 20px;
}

.form-group label {
  display: block;
  margin-bottom: 8px;
  font-weight: 600;
  color: #495057;
}

.form-input,
.form-textarea {
  width: 100%;
  padding: 12px 16px;
  border: 2px solid #dee2e6;
  border-radius: 8px;
  font-size: 14px;
  transition: border-color 0.3s ease;
  box-sizing: border-box;
}

.form-input:focus,
.form-textarea:focus {
  outline: none;
  border-color: #007bff;
  box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.1);
}

.form-textarea {
  resize: vertical;
  min-height: 120px;
  font-family: inherit;
}

.form-actions {
  display: flex;
  gap: 15px;
  justify-content: center;
}

.submit-btn,
.reset-btn {
  padding: 12px 24px;
  border: none;
  border-radius: 8px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
}

.submit-btn {
  background: #28a745;
  color: white;
}

.submit-btn:hover:not(:disabled) {
  background: #218838;
  transform: translateY(-2px);
}

.submit-btn:disabled {
  background: #6c757d;
  cursor: not-allowed;
  transform: none;
}

.reset-btn {
  background: #6c757d;
  color: white;
}

.reset-btn:hover {
  background: #5a6268;
  transform: translateY(-2px);
}

.editor-info {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 15px;
  background: white;
  border-radius: 8px;
  border: 1px solid #dee2e6;
}

.info-item {
  display: flex;
  align-items: center;
  gap: 8px;
}

.info-label {
  font-weight: 600;
  color: #495057;
}

.info-value {
  font-weight: 500;
}

.info-value.valid {
  color: #28a745;
}

.info-value.invalid {
  color: #dc3545;
}

@media (max-width: 768px) {
  .form-actions {
    flex-direction: column;
  }

  .editor-info {
    flex-direction: column;
    gap: 10px;
  }
}
</style>
