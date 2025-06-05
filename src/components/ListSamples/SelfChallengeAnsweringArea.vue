<template>
  <div class="answering-area">
    <h2>🎯 實作練習區 - v-for 列表渲染</h2>
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
        <!-- 🎯 任務：在這裡使用 v-for 渲染學生列表 -->
        <!-- 提示：使用 filteredStudents 作為資料來源 -->
        <!--
        <div v-for="student in filteredStudents" :key="student.id" class="student-card">
          <h4>{{ student.name }}</h4>
          <p>科目：{{ student.subject }}</p>
          <p>分數：{{ student.score }}</p>
          <button @click="removeStudent(student.id)" class="btn btn-danger">刪除</button>
          <button @click="editStudent(student)" class="btn btn-warning">編輯</button>
        </div>
        -->
      </div>
    </div>

    <!-- 任務二：新增學生表單 -->
    <div class="task-section">
      <h3>➕ 任務二：新增學生</h3>
      <div class="add-form">
        <input v-model="newStudent.name" placeholder="學生姓名" class="form-input">
        <input v-model="newStudent.subject" placeholder="科目" class="form-input">
        <input v-model.number="newStudent.score" type="number" placeholder="分數" class="form-input">
        <button @click="addStudent" class="btn btn-success">新增學生</button>
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
      </div>
    </div>

    <!-- 編輯學生表單 -->
    <div v-if="editingId" class="edit-form">
      <h3>✏️ 編輯學生</h3>
      <input v-model="editForm.name" placeholder="學生姓名" class="form-input">
      <input v-model="editForm.subject" placeholder="科目" class="form-input">
      <input v-model.number="editForm.score" type="number" placeholder="分數" class="form-input">
      <button @click="saveEdit" class="btn btn-success">儲存</button>
      <button @click="cancelEdit" class="btn btn-secondary">取消</button>
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

// 🎯 任務：實作 filteredStudents 計算屬性
// eslint-disable-next-line no-unused-vars
const filteredStudents = computed(() => {
  // 請在這裡實作篩選邏輯
  // 根據 showPassed 的值決定是否只顯示及格學生（分數 >= 60）
  return students.value
})

// 🎯 任務：實作 addStudent 方法
const addStudent = () => {
  // 請在這裡實作新增學生的邏輯
  // 1. 驗證表單資料
  // 2. 生成新的 ID
  // 3. 加入學生列表
  // 4. 重置表單
  console.log('請實作新增學生功能')
}

// 🎯 任務：實作 removeStudent 方法
// eslint-disable-next-line no-unused-vars
const removeStudent = (studentId) => {
  // 請在這裡實作刪除學生的邏輯
  // 使用 filter 方法移除指定 ID 的學生
  console.log('請實作刪除學生功能')
}

// 🎯 任務：實作 editStudent 方法
// eslint-disable-next-line no-unused-vars
const editStudent = (student) => {
  // 請在這裡實作開始編輯的邏輯
  // 1. 設定 editingId
  // 2. 複製學生資料到 editForm
  console.log('請實作編輯學生功能')
}

// 🎯 任務：實作 saveEdit 方法
const saveEdit = () => {
  // 請在這裡實作儲存編輯的邏輯
  // 1. 找到對應的學生
  // 2. 更新學生資料
  // 3. 重置編輯狀態
}

// 🎯 任務：實作 cancelEdit 方法
const cancelEdit = () => {
  // 請在這裡實作取消編輯的邏輯
  // 重置編輯狀態
}

// 排序功能（已提供）
const sortByScore = () => {
  students.value.sort((a, b) => b.score - a.score)
}

// 🎯 任務：實作統計計算屬性
const totalStudents = computed(() => {
  // 回傳學生總數
  return 0
})

const passedCount = computed(() => {
  // 回傳及格學生數量（分數 >= 60）
  return 0
})

const averageScore = computed(() => {
  // 回傳平均分數（保留一位小數）
  return 0
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
}

.btn-primary {
  background: #007bff;
  color: white;
}

.btn-secondary {
  background: #6c757d;
  color: white;
}

.btn-success {
  background: #28a745;
  color: white;
}

.btn-warning {
  background: #ffc107;
  color: black;
}

.btn-danger {
  background: #dc3545;
  color: white;
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
}

.add-form,
.edit-form {
  display: flex;
  gap: 1rem;
  align-items: center;
  flex-wrap: wrap;
}

.form-input {
  padding: 0.5rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  min-width: 150px;
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
}

.stat-number {
  font-size: 2rem;
  font-weight: bold;
  color: #007bff;
  margin: 0;
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
