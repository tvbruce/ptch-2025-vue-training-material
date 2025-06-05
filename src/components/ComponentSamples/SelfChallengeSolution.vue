<template>
  <div class="answering-area">
    <h2>🎯 參考答案 - Component 組件化</h2>
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
        <!-- 使用 TaskForm 組件 -->
        <TaskForm @add-task="handleAddTask" />
      </div>
    </div>

    <!-- 任務三：任務篩選 -->
    <div class="task-section">
      <h3>🔍 任務三：任務篩選</h3>
      <div class="filter-container">
        <button v-for="filter in filters" :key="filter.value" @click="currentFilter = filter.value"
          :class="['filter-btn', { active: currentFilter === filter.value }]">
          {{ filter.label }}
        </button>
      </div>
    </div>

    <!-- 任務四：任務列表 -->
    <div class="task-section">
      <h3>📋 任務四：任務列表</h3>
      <div class="tasks-container">
        <!-- 使用 TaskItem 組件 -->
        <div v-if="filteredTasks.length === 0" class="no-tasks">
          沒有符合條件的任務
        </div>
        <div v-else class="tasks-grid">
          <TaskItem v-for="task in filteredTasks" :key="task.id" :task="task" @toggle-complete="handleToggleComplete"
            @delete-task="handleDeleteTask" />
        </div>
      </div>
    </div>

    <!-- 任務五：可重用組件 -->
    <div class="task-section">
      <h3>🎨 任務五：可重用卡片組件</h3>
      <div class="card-demo">
        <!-- 使用 Card 組件展示不同樣式 -->
        <div class="demo-grid">
          <SolutionCard title="基本卡片" color="primary" size="medium" :bordered="true">
            <p>這是一個功能豐富的卡片組件，展示了預設插槽的使用。</p>
            <p>可以在這裡放置任何內容，支援多種樣式和功能。</p>
          </SolutionCard>

          <SolutionCard title="進階卡片" subtitle="包含多個插槽" color="success" :elevated="true">
            <template #header>
              <div class="custom-header">
                <h4>🎯 自定義標題</h4>
                <span class="badge">NEW</span>
              </div>
            </template>
            <p>這個卡片使用了自定義的 header 插槽。</p>
            <ul>
              <li>多插槽支援</li>
              <li>響應式設計</li>
              <li>動畫效果</li>
            </ul>
            <template #footer>
              <div class="card-actions">
                <button class="btn btn-primary">詳細資訊</button>
                <button class="btn btn-secondary">分享</button>
              </div>
            </template>
          </SolutionCard>

          <SolutionCard title="統計卡片" subtitle="即時資料展示" color="info" :expandable="true">
            <template #header>
              <div class="stat-header">
                <h4>📈 任務統計</h4>
              </div>
            </template>
            <div class="mini-stats">
              <div class="mini-stat">
                <span class="number">{{ totalTasks }}</span>
                <span class="label">總數</span>
              </div>
              <div class="mini-stat">
                <span class="number">{{ completedCount }}</span>
                <span class="label">已完成</span>
              </div>
              <div class="mini-stat">
                <span class="number">{{ completionRate }}%</span>
                <span class="label">完成率</span>
              </div>
            </div>
            <template #expanded>
              <div class="detailed-stats">
                <h5>詳細統計</h5>
                <p>高優先級任務：{{tasks.filter(t => t.priority === 'high').length}} 個</p>
                <p>中優先級任務：{{tasks.filter(t => t.priority === 'medium').length}} 個</p>
                <p>低優先級任務：{{tasks.filter(t => t.priority === 'low').length}} 個</p>
              </div>
            </template>
            <template #footer>
              <small>即時更新的統計資料 • 點擊箭頭展開詳細</small>
            </template>
          </SolutionCard>
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
        <li>組件檔案放在 components/ComponentSamples/components/SelfChallengeSolution/ 目錄下</li>
        <li>記得在父組件中 import 並註冊子組件</li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import TaskForm from './components/SelfChallengeSolution/TaskForm.vue'
import TaskItem from './components/SelfChallengeSolution/TaskItem.vue'
import SolutionCard from './components/SelfChallengeSolution/SolutionCard.vue'

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
  },
  {
    id: 4,
    title: '準備期末考試',
    description: '複習所有課程內容',
    priority: 'high',
    completed: false,
    createdAt: new Date()
  },
  {
    id: 5,
    title: '小組專案會議',
    description: '討論專案進度和分工',
    priority: 'medium',
    completed: true,
    createdAt: new Date()
  }
])

// 篩選器
const currentFilter = ref('all')
const filters = [
  { value: 'all', label: '全部' },
  { value: 'pending', label: '待完成' },
  { value: 'completed', label: '已完成' },
  { value: 'high', label: '高優先級' },
  { value: 'medium', label: '中優先級' },
  { value: 'low', label: '低優先級' }
]

// 統計計算屬性
const totalTasks = computed(() => {
  return tasks.value.length
})

const completedCount = computed(() => {
  return tasks.value.filter(task => task.completed).length
})

const pendingCount = computed(() => {
  return tasks.value.filter(task => !task.completed).length
})

const completionRate = computed(() => {
  if (totalTasks.value === 0) return 0
  return Math.round((completedCount.value / totalTasks.value) * 100)
})

// 篩選計算屬性
const filteredTasks = computed(() => {
  const filter = currentFilter.value

  if (filter === 'all') {
    return tasks.value
  } else if (filter === 'completed') {
    return tasks.value.filter(task => task.completed)
  } else if (filter === 'pending') {
    return tasks.value.filter(task => !task.completed)
  } else {
    // 按優先級篩選
    return tasks.value.filter(task => task.priority === filter)
  }
})

// 任務管理方法
const generateTaskId = () => {
  return Math.max(0, ...tasks.value.map(task => task.id)) + 1
}

const toggleComplete = (taskId) => {
  const task = tasks.value.find(task => task.id === taskId)
  if (task) {
    task.completed = !task.completed
  }
}

const deleteTask = (taskId) => {
  const confirmed = confirm('確定要刪除這個任務嗎？')
  if (confirmed) {
    const index = tasks.value.findIndex(task => task.id === taskId)
    if (index !== -1) {
      tasks.value.splice(index, 1)
    }
  }
}

// 組件事件處理方法
const handleAddTask = (taskData) => {
  const newTask = {
    id: generateTaskId(),
    title: taskData.title,
    description: taskData.description,
    priority: taskData.priority,
    completed: false,
    createdAt: new Date()
  }

  tasks.value.unshift(newTask)
}

const handleToggleComplete = (taskId) => {
  toggleComplete(taskId)
}

const handleDeleteTask = (taskId) => {
  deleteTask(taskId)
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
  transition: transform 0.2s ease;
}

.stat-card:hover {
  transform: translateY(-2px);
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

.filter-container {
  display: flex;
  gap: 0.5rem;
  flex-wrap: wrap;
}

.filter-btn {
  padding: 0.5rem 1rem;
  border: 2px solid #dee2e6;
  background: white;
  border-radius: 20px;
  cursor: pointer;
  transition: all 0.3s ease;
  font-size: 0.9rem;
}

.filter-btn:hover {
  border-color: #20c997;
  transform: translateY(-1px);
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
  font-size: 1.1rem;
}

.tasks-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1rem;
}

.card-demo {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.demo-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1.5rem;
}

.custom-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.custom-header h4 {
  margin: 0;
  color: white;
}

.badge {
  background: rgba(255, 255, 255, 0.2);
  padding: 0.25rem 0.5rem;
  border-radius: 12px;
  font-size: 0.7rem;
  font-weight: bold;
}

.stat-header h4 {
  margin: 0;
  color: white;
}

.mini-stats {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  margin: 1rem 0;
}

.mini-stat {
  text-align: center;
  padding: 1rem;
  background: #f8f9fa;
  border-radius: 8px;
}

.mini-stat .number {
  display: block;
  font-size: 1.5rem;
  font-weight: bold;
  color: #495057;
}

.mini-stat .label {
  display: block;
  font-size: 0.8rem;
  color: #6c757d;
  margin-top: 0.25rem;
}

.card-actions {
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

.btn:hover {
  transform: translateY(-1px);
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}

.btn-primary {
  background: #007bff;
  color: white;
}

.btn-primary:hover {
  background: #0056b3;
}

.btn-secondary {
  background: #6c757d;
  color: white;
}

.btn-secondary:hover {
  background: #545b62;
}

.detailed-stats {
  background: #f8f9fa;
  padding: 1rem;
  border-radius: 8px;
  margin-top: 1rem;
}

.detailed-stats h5 {
  margin: 0 0 1rem 0;
  color: #495057;
  font-size: 1rem;
}

.detailed-stats p {
  margin: 0.5rem 0;
  color: #6c757d;
  font-size: 0.9rem;
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
  .filter-container {
    justify-content: center;
  }

  .tasks-grid,
  .demo-grid {
    grid-template-columns: 1fr;
  }

  .mini-stats {
    grid-template-columns: 1fr;
  }

  .card-actions {
    flex-direction: column;
  }
}
</style>
