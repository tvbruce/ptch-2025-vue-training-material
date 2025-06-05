<template>
  <div class="answering-area">
    <h2>🎯 參考答案 - v-for 列表渲染</h2>
    <p class="description">
      📝 <strong>任務：</strong>建立學生成績管理系統，實作 v-for 列表渲染的各種功能
    </p>

    <!-- 任務一：學生列表渲染 -->
    <div class="task-section">
      <h3>📋 任務一：學生列表渲染</h3>
      <div class="controls">
        <button @click="sortByScore" class="btn btn-primary">按分數排序</button>
        <button @click="showPassed = !showPassed" class="btn btn-secondary">
          {{ showPassed ? '顯示全部' : '只顯示及格' }}
        </button>
      </div>

      <div class="student-grid">
        <div v-for="student in filteredStudents" :key="student.id" class="student-card"
          :class="{ 'passed': student.score >= 60, 'failed': student.score < 60 }">
          <h4>{{ student.name }}</h4>
          <p>科目：{{ student.subject }}</p>
          <p>分數：{{ student.score }}</p>
          <div class="card-actions">
            <button @click="removeStudent(student.id)" class="btn btn-danger">刪除</button>
            <button @click="editStudent(student)" class="btn btn-warning">編輯</button>
          </div>
        </div>
      </div>

      <div v-if="filteredStudents.length === 0" class="empty-message">
        <p>{{ showPassed ? '沒有及格的學生' : '沒有學生資料' }}</p>
      </div>
    </div>

    <!-- 任務二：新增學生表單 -->
    <div class="task-section">
      <h3>➕ 任務二：新增學生</h3>
      <div class="add-form">
        <input v-model="newStudent.name" placeholder="學生姓名" class="form-input"
          :class="{ 'error': newStudentErrors.name }">
        <input v-model="newStudent.subject" placeholder="科目" class="form-input"
          :class="{ 'error': newStudentErrors.subject }">
        <input v-model.number="newStudent.score" type="number" placeholder="分數" class="form-input" min="0" max="100"
          :class="{ 'error': newStudentErrors.score }">
        <button @click="addStudent" class="btn btn-success" :disabled="!canAddStudent">新增學生</button>
      </div>
      <div v-if="Object.keys(newStudentErrors).length > 0" class="error-messages">
        <p v-for="error in newStudentErrors" :key="error" class="error-text">{{ error }}</p>
      </div>
    </div>

    <!-- 任務三：統計資料 -->
    <div class="task-section">
      <h3>📊 任務三：統計資料</h3>
      <div class="stats-grid">
        <div class="stat-card">
          <h4>總學生數</h4>
          <p class="stat-number">{{ totalStudents }}</p>
        </div>
        <div class="stat-card">
          <h4>及格人數</h4>
          <p class="stat-number">{{ passedCount }}</p>
        </div>
        <div class="stat-card">
          <h4>平均分數</h4>
          <p class="stat-number">{{ averageScore }}</p>
        </div>
        <div class="stat-card">
          <h4>及格率</h4>
          <p class="stat-number">{{ passRate }}%</p>
        </div>
      </div>
    </div>

    <!-- 編輯學生表單 -->
    <div v-if="editingId" class="edit-form-section">
      <h3>✏️ 編輯學生</h3>
      <div class="edit-form">
        <input v-model="editForm.name" placeholder="學生姓名" class="form-input" :class="{ 'error': editFormErrors.name }">
        <input v-model="editForm.subject" placeholder="科目" class="form-input"
          :class="{ 'error': editFormErrors.subject }">
        <input v-model.number="editForm.score" type="number" placeholder="分數" class="form-input" min="0" max="100"
          :class="{ 'error': editFormErrors.score }">
        <button @click="saveEdit" class="btn btn-success" :disabled="!canSaveEdit">儲存</button>
        <button @click="cancelEdit" class="btn btn-secondary">取消</button>
      </div>
      <div v-if="Object.keys(editFormErrors).length > 0" class="error-messages">
        <p v-for="error in editFormErrors" :key="error" class="error-text">{{ error }}</p>
      </div>
    </div>

    <!-- 開發提示 -->
    <div class="hint-section">
      <h4>💡 開發提示</h4>
      <ul>
        <li>使用 v-for 渲染列表時記得加上 :key 屬性</li>
        <li>filteredStudents 計算屬性需要根據 showPassed 狀態篩選</li>
        <li>新增學生時需要生成唯一的 ID</li>
        <li>編輯功能需要複製資料避免直接修改原始物件</li>
        <li>統計功能使用 computed 計算屬性實作</li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 學生資料
const students = ref([
  { id: 1, name: '小明', subject: '數學', score: 85 },
  { id: 2, name: '小華', subject: '英文', score: 92 },
  { id: 3, name: '小美', subject: '數學', score: 45 },
  { id: 4, name: '小強', subject: '物理', score: 78 },
  { id: 5, name: '小芳', subject: '化學', score: 55 }
])

// 新學生表單
const newStudent = ref({
  name: '',
  subject: '',
  score: 0
})

// 編輯相關狀態
const editingId = ref(null)
const editForm = ref({})

// 控制狀態
const showPassed = ref(false)

// 篩選學生列表
const filteredStudents = computed(() => {
  if (showPassed.value) {
    return students.value.filter(student => student.score >= 60)
  }
  return students.value
})

// 表單驗證
const newStudentErrors = computed(() => {
  const errors = {}
  if (!newStudent.value.name?.trim()) {
    errors.name = '請輸入學生姓名'
  }
  if (!newStudent.value.subject?.trim()) {
    errors.subject = '請輸入科目'
  }
  if (newStudent.value.score < 0 || newStudent.value.score > 100) {
    errors.score = '分數必須在 0-100 之間'
  }
  return errors
})

const canAddStudent = computed(() => {
  return Object.keys(newStudentErrors.value).length === 0 &&
    newStudent.value.name?.trim() &&
    newStudent.value.subject?.trim()
})

const editFormErrors = computed(() => {
  const errors = {}
  if (!editForm.value.name?.trim()) {
    errors.name = '請輸入學生姓名'
  }
  if (!editForm.value.subject?.trim()) {
    errors.subject = '請輸入科目'
  }
  if (editForm.value.score < 0 || editForm.value.score > 100) {
    errors.score = '分數必須在 0-100 之間'
  }
  return errors
})

const canSaveEdit = computed(() => {
  return Object.keys(editFormErrors.value).length === 0 &&
    editForm.value.name?.trim() &&
    editForm.value.subject?.trim()
})

// 新增學生
const addStudent = () => {
  if (!canAddStudent.value) return

  // 生成新的 ID
  const newId = Math.max(...students.value.map(s => s.id), 0) + 1

  // 建立新學生物件
  const student = {
    id: newId,
    name: newStudent.value.name.trim(),
    subject: newStudent.value.subject.trim(),
    score: Number(newStudent.value.score)
  }

  // 加入學生列表
  students.value.push(student)

  // 重置表單
  newStudent.value = {
    name: '',
    subject: '',
    score: 0
  }
}

// 刪除學生
const removeStudent = (studentId) => {
  if (confirm('確定要刪除這位學生嗎？')) {
    students.value = students.value.filter(student => student.id !== studentId)
    // 如果正在編輯這位學生，取消編輯
    if (editingId.value === studentId) {
      cancelEdit()
    }
  }
}

// 開始編輯學生
const editStudent = (student) => {
  editingId.value = student.id
  // 深拷貝學生資料，避免直接修改原始資料
  editForm.value = {
    name: student.name,
    subject: student.subject,
    score: student.score
  }
}

// 儲存編輯
const saveEdit = () => {
  if (!canSaveEdit.value) return

  // 找到對應的學生
  const studentIndex = students.value.findIndex(s => s.id === editingId.value)
  if (studentIndex !== -1) {
    // 更新學生資料
    students.value[studentIndex] = {
      ...students.value[studentIndex],
      name: editForm.value.name.trim(),
      subject: editForm.value.subject.trim(),
      score: Number(editForm.value.score)
    }
  }

  // 重置編輯狀態
  cancelEdit()
}

// 取消編輯
const cancelEdit = () => {
  editingId.value = null
  editForm.value = {}
}

// 排序功能
const sortByScore = () => {
  students.value.sort((a, b) => b.score - a.score)
}

// 統計計算屬性
const totalStudents = computed(() => {
  return students.value.length
})

const passedCount = computed(() => {
  return students.value.filter(student => student.score >= 60).length
})

const averageScore = computed(() => {
  if (students.value.length === 0) return 0
  const total = students.value.reduce((sum, student) => sum + student.score, 0)
  return (total / students.value.length).toFixed(1)
})

const passRate = computed(() => {
  if (students.value.length === 0) return 0
  return ((passedCount.value / totalStudents.value) * 100).toFixed(1)
})
</script>

<style scoped>
.answering-area {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

.task-section {
  background: #f8f9fa;
  padding: 2rem;
  border-radius: 8px;
  margin: 2rem 0;
  border-left: 4px solid #007bff;
}

.controls {
  margin-bottom: 1rem;
}

.btn {
  padding: 0.5rem 1rem;
  margin-right: 0.5rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.2s;
}

.btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.btn-primary {
  background: #007bff;
  color: white;
}

.btn-primary:hover:not(:disabled) {
  background: #0056b3;
}

.btn-secondary {
  background: #6c757d;
  color: white;
}

.btn-secondary:hover:not(:disabled) {
  background: #545b62;
}

.btn-success {
  background: #28a745;
  color: white;
}

.btn-success:hover:not(:disabled) {
  background: #1e7e34;
}

.btn-warning {
  background: #ffc107;
  color: black;
}

.btn-warning:hover:not(:disabled) {
  background: #e0a800;
}

.btn-danger {
  background: #dc3545;
  color: white;
}

.btn-danger:hover:not(:disabled) {
  background: #c82333;
}

.student-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1rem;
  margin-top: 1rem;
}

.student-card {
  background: white;
  padding: 1rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s;
}

.student-card:hover {
  transform: translateY(-2px);
}

.student-card.passed {
  border-left: 4px solid #28a745;
}

.student-card.failed {
  border-left: 4px solid #dc3545;
}

.card-actions {
  margin-top: 1rem;
  display: flex;
  gap: 0.5rem;
}

.card-actions .btn {
  margin-right: 0;
  flex: 1;
}

.add-form,
.edit-form {
  display: flex;
  gap: 1rem;
  align-items: center;
  flex-wrap: wrap;
}

.edit-form-section {
  background: #fff3cd;
  padding: 2rem;
  border-radius: 8px;
  margin: 2rem 0;
  border-left: 4px solid #ffc107;
}

.form-input {
  padding: 0.5rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  min-width: 150px;
  transition: border-color 0.2s;
}

.form-input:focus {
  border-color: #007bff;
  outline: none;
}

.form-input.error {
  border-color: #dc3545;
}

.error-messages {
  margin-top: 0.5rem;
}

.error-text {
  color: #dc3545;
  font-size: 0.875rem;
  margin: 0.25rem 0;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
  margin-top: 1rem;
}

.stat-card {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  text-align: center;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s;
}

.stat-card:hover {
  transform: translateY(-2px);
}

.stat-number {
  font-size: 2rem;
  font-weight: bold;
  color: #007bff;
  margin: 0;
}

.empty-message {
  text-align: center;
  padding: 2rem;
  color: #6c757d;
  font-style: italic;
}

.hint-section {
  background: #fff3cd;
  padding: 1.5rem;
  border-radius: 8px;
  margin-top: 2rem;
  border-left: 4px solid #ffc107;
}

.hint-section ul {
  margin: 0.5rem 0;
  padding-left: 1.5rem;
}

.hint-section li {
  margin-bottom: 0.5rem;
}
</style>
