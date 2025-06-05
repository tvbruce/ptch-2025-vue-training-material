<template>
  <div class="answering-area">
    <h2>🎯 實作練習區 - Component 組件化</h2>
    <p class="description">
      📝 <strong>任務：</strong>建立一個任務管理系統，實作組件化開發的核心概念
    </p>

    <!-- 任務一：任務統計 -->
    <div class="task-section">
      <h3>📊 任務一：任務統計</h3>
      <div class="stats-container">
        <div class="stat-card">
          <h4>總任務</h4>
          <span class="stat-number">{{ totalTasks }}</span>
        </div>
        <div class="stat-card completed">
          <h4>已完成</h4>
          <span class="stat-number">{{ completedCount }}</span>
        </div>
        <div class="stat-card pending">
          <h4>待完成</h4>
          <span class="stat-number">{{ pendingCount }}</span>
        </div>
        <div class="stat-card rate">
          <h4>完成率</h4>
          <span class="stat-number">{{ completionRate }}%</span>
        </div>
      </div>
    </div>

    <!-- 任務二：新增任務表單 -->
    <div class="task-section">
      <h3>➕ 任務二：新增任務</h3>
      <div class="form-container">
        <!-- 🎯 任務：在這裡使用 TaskForm 組件 -->
        <!-- 提示：<TaskForm @add-task="handleAddTask" /> -->
        <div class="placeholder-form">
          <p>請建立 TaskForm 組件並在這裡使用</p>
          <div class="temp-form">
            <input v-model="newTask.title" placeholder="任務標題" class="form-input">
            <input v-model="newTask.description" placeholder="任務描述" class="form-input">
            <select v-model="newTask.priority" class="form-select">
              <option value="low">低優先級</option>
              <option value="medium">中優先級</option>
              <option value="high">高優先級</option>
            </select>
            <button @click="addTask" class="btn btn-primary">新增任務</button>
          </div>
        </div>
      </div>
    </div>

    <!-- 任務三：任務篩選 -->
    <div class="task-section">
      <h3>🔍 任務三：任務篩選</h3>
      <div class="filter-container">
        <!-- 🎯 任務：實作篩選按鈕 -->
        <!-- 提示：使用 v-for 遍歷 filters，使用 @click 和 :class 實作切換 -->
        <div class="filter-placeholder">
          <p>請實作篩選按鈕功能</p>
          <div class="temp-filters">
            <button class="filter-btn active">全部</button>
            <button class="filter-btn">待完成</button>
            <button class="filter-btn">已完成</button>
            <button class="filter-btn">高優先級</button>
          </div>
        </div>
      </div>
    </div>

    <!-- 任務四：任務列表 -->
    <div class="task-section">
      <h3>📋 任務四：任務列表</h3>
      <div class="tasks-container">
        <!-- 🎯 任務：在這裡使用 TaskItem 組件 -->
        <!-- 提示：
        <TaskItem
          v-for="task in filteredTasks"
          :key="task.id"
          :task="task"
          @toggle-complete="handleToggleComplete"
          @delete-task="handleDeleteTask"
        />
        -->
        <div v-if="filteredTasks.length === 0" class="no-tasks">
          沒有符合條件的任務
        </div>
        <div v-else class="tasks-grid">
          <div v-for="task in filteredTasks" :key="task.id" class="task-card-placeholder">
            <p>請建立 TaskItem 組件來顯示任務：{{ task.title }}</p>
            <div class="temp-task-card">
              <h5>{{ task.title }}</h5>
              <p>{{ task.description }}</p>
              <span :class="['priority', task.priority]">{{ task.priority }}</span>
              <div class="task-actions">
                <button @click="toggleComplete(task.id)" class="btn btn-sm">
                  {{ task.completed ? '取消完成' : '標記完成' }}
                </button>
                <button @click="deleteTask(task.id)" class="btn btn-danger btn-sm">刪除</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- 任務五：可重用組件 -->
    <div class="task-section">
      <h3>🎨 任務五：可重用卡片組件</h3>
      <div class="card-demo">
        <!-- 🎯 任務：在這裡使用 Card 組件 -->
        <!-- 提示：
        <Card title="範例卡片" color="blue">
          <template #header>
            <h4>自定義標題</h4>
          </template>
<p>這是卡片內容</p>
<template #footer>
            <button>操作按鈕</button>
          </template>
</Card>
-->
        <div class="placeholder-card">
          <p>請建立 Card 組件並在這裡使用插槽功能</p>
          <div class="temp-card">
            <div class="card-header">範例卡片標題</div>
            <div class="card-body">這裡應該是插槽內容</div>
            <div class="card-footer">這裡是底部插槽</div>
          </div>
        </div>
      </div>
    </div>

    <!-- 開發提示 -->
    <div class="hint-section">
      <h4>💡 開發提示</h4>
      <ul>
        <li>TaskForm 組件：接收表單資料，emit add-task 事件</li>
        <li>TaskItem 組件：接收 task prop，emit toggle-complete 和 delete-task 事件</li>
        <li>Card 組件：使用具名插槽 header、default、footer</li>
        <li>組件檔案放在 components/ComponentSamples/components/SelfChallengeAnswering/ 目錄下</li>
        <li>記得在父組件中 import 並註冊子組件</li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 任務資料
const tasks = ref([
  {
    id: 1,
    title: '完成 Vue.js 教學',
    description: '學習 Vue3 的基本概念和語法',
    priority: 'high',
    completed: false,
    createdAt: new Date()
  },
  {
    id: 2,
    title: '寫程式作業',
    description: '完成本週的程式設計作業',
    priority: 'medium',
    completed: true,
    createdAt: new Date()
  },
  {
    id: 3,
    title: '複習資料結構',
    description: '準備下週的資料結構測驗',
    priority: 'low',
    completed: false,
    createdAt: new Date()
  }
])

// 新任務表單資料
const newTask = ref({
  title: '',
  description: '',
  priority: 'medium'
})

// 🎯 任務：定義篩選器資料
// 提示：使用 ref 定義當前篩選條件和篩選選項
// const currentFilter = ref('all')
// const filters = [
//   { value: 'all', label: '全部' },
//   { value: 'pending', label: '待完成' },
//   { value: 'completed', label: '已完成' },
//   { value: 'high', label: '高優先級' },
//   { value: 'medium', label: '中優先級' },
//   { value: 'low', label: '低優先級' }
// ]

// 🎯 任務：實作統計計算屬性
const totalTasks = computed(() => {
  // 請在這裡實作總任務數計算
  return tasks.value.length
})

const completedCount = computed(() => {
  // 請在這裡實作已完成任務數計算
  return 0
})

const pendingCount = computed(() => {
  // 請在這裡實作待完成任務數計算
  return 0
})

const completionRate = computed(() => {
  // 請在這裡實作完成率計算
  return 0
})

// 🎯 任務：實作篩選計算屬性
const filteredTasks = computed(() => {
  // 請在這裡實作任務篩選邏輯
  // 根據 currentFilter.value 篩選任務
  return tasks.value
})

// 🎯 任務：實作任務管理方法
const addTask = () => {
  // 請在這裡實作新增任務邏輯
  // 1. 驗證表單資料
  // 2. 生成新的任務 ID
  // 3. 加入任務列表
  // 4. 重置表單
  console.log('請實作新增任務功能')
}

const toggleComplete = (taskId) => {
  // 請在這裡實作切換完成狀態邏輯
  // 找到對應任務並切換其 completed 狀態
  console.log('請實作切換完成狀態功能', taskId)
}

const deleteTask = (taskId) => {
  // 請在這裡實作刪除任務邏輯
  // 從任務列表中移除指定 ID 的任務
  console.log('請實作刪除任務功能', taskId)
}

// 🎯 任務：實作組件事件處理方法
// eslint-disable-next-line no-unused-vars
const handleAddTask = (taskData) => {
  // 請在這裡實作處理 TaskForm 組件發送的 add-task 事件
  console.log('請實作處理新增任務事件')
}

// eslint-disable-next-line no-unused-vars
const handleToggleComplete = (taskId) => {
  // 請在這裡實作處理 TaskItem 組件發送的 toggle-complete 事件
  console.log('請實作處理切換完成事件')
}

// eslint-disable-next-line no-unused-vars
const handleDeleteTask = (taskId) => {
  // 請在這裡實作處理 TaskItem 組件發送的 delete-task 事件
  console.log('請實作處理刪除任務事件')
}
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
  border-left: 4px solid #20c997;
}

.stats-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
}

.stat-card {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  text-align: center;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  border-left: 4px solid #007bff;
}

.stat-card.completed {
  border-left-color: #28a745;
}

.stat-card.pending {
  border-left-color: #ffc107;
}

.stat-card.rate {
  border-left-color: #17a2b8;
}

.stat-card h4 {
  margin: 0 0 0.5rem 0;
  color: #6c757d;
  font-size: 0.9rem;
}

.stat-number {
  font-size: 2rem;
  font-weight: bold;
  color: #495057;
}

.form-container {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.placeholder-form {
  text-align: center;
  padding: 2rem;
  border: 2px dashed #dee2e6;
  border-radius: 8px;
  color: #6c757d;
}

.temp-form {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr auto;
  gap: 1rem;
  margin-top: 1rem;
  align-items: center;
}

.form-input,
.form-select {
  padding: 0.5rem;
  border: 1px solid #dee2e6;
  border-radius: 4px;
}

.filter-container {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.filter-placeholder {
  text-align: center;
  padding: 1rem;
  border: 2px dashed #dee2e6;
  border-radius: 8px;
  color: #6c757d;
}

.temp-filters {
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
  justify-content: center;
  margin-top: 1rem;
}

.filter-btn {
  padding: 0.5rem 1rem;
  border: 2px solid #dee2e6;
  background: white;
  border-radius: 20px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.filter-btn:hover {
  border-color: #20c997;
}

.filter-btn.active {
  background: #20c997;
  color: white;
  border-color: #20c997;
}

.tasks-container {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.no-tasks {
  text-align: center;
  padding: 3rem;
  color: #6c757d;
  font-style: italic;
}

.tasks-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1rem;
}

.task-card-placeholder {
  border: 2px dashed #dee2e6;
  border-radius: 8px;
  padding: 1rem;
  text-align: center;
  color: #6c757d;
}

.temp-task-card {
  background: #f8f9fa;
  padding: 1rem;
  border-radius: 4px;
  margin-top: 1rem;
}

.temp-task-card h5 {
  margin: 0 0 0.5rem 0;
  color: #495057;
}

.temp-task-card p {
  margin: 0 0 0.5rem 0;
  color: #6c757d;
  font-size: 0.9rem;
}

.priority {
  display: inline-block;
  padding: 0.2rem 0.5rem;
  border-radius: 12px;
  font-size: 0.8rem;
  font-weight: bold;
  text-transform: uppercase;
}

.priority.high {
  background: #f8d7da;
  color: #721c24;
}

.priority.medium {
  background: #fff3cd;
  color: #856404;
}

.priority.low {
  background: #d4edda;
  color: #155724;
}

.task-actions {
  display: flex;
  gap: 0.5rem;
  margin-top: 1rem;
}

.card-demo {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.placeholder-card {
  text-align: center;
  padding: 2rem;
  border: 2px dashed #dee2e6;
  border-radius: 8px;
  color: #6c757d;
}

.temp-card {
  background: #f8f9fa;
  border-radius: 8px;
  overflow: hidden;
  margin-top: 1rem;
  max-width: 300px;
  margin-left: auto;
  margin-right: auto;
}

.card-header {
  background: #20c997;
  color: white;
  padding: 1rem;
  font-weight: bold;
}

.card-body {
  padding: 1rem;
}

.card-footer {
  background: #e9ecef;
  padding: 0.5rem 1rem;
  font-size: 0.9rem;
  color: #6c757d;
}

.btn {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9rem;
  transition: background-color 0.3s ease;
}

.btn-primary {
  background: #007bff;
  color: white;
}

.btn-danger {
  background: #dc3545;
  color: white;
}

.btn-sm {
  padding: 0.25rem 0.5rem;
  font-size: 0.8rem;
}

.btn:hover {
  opacity: 0.9;
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

@media (max-width: 768px) {
  .temp-form {
    grid-template-columns: 1fr;
  }

  .filter-container {
    justify-content: center;
  }

  .tasks-grid {
    grid-template-columns: 1fr;
  }
}
</style>
