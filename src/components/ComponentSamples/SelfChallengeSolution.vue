<template>
    <div class="self-challenge-solution">
        <h2>🎯 自我試煉解答 - 組件化開發</h2>
        <p class="route-info">📍 路徑：/ComponentSamples/SelfChallengeSolution.vue</p>

        <div class="task-manager">
            <h3>📋 任務管理系統</h3>

            <!-- 任務統計面板 -->
            <div class="stats-panel">
                <div class="stat-card">
                    <div class="stat-value">{{ tasks.length }}</div>
                    <div class="stat-label">總任務數</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">{{ completedCount }}</div>
                    <div class="stat-label">已完成</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">{{ pendingCount }}</div>
                    <div class="stat-label">待完成</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">{{ completionRate }}%</div>
                    <div class="stat-label">完成率</div>
                </div>
            </div>

            <!-- 新增任務表單 -->
            <TaskForm @add-task="handleAddTask" />

            <!-- 任務篩選器 -->
            <div class="filter-panel">
                <h4>🔍 任務篩選</h4>
                <div class="filter-buttons">
                    <button v-for="filter in filters" :key="filter.value" @click="currentFilter = filter.value"
                        class="filter-btn" :class="{ active: currentFilter === filter.value }">
                        {{ filter.label }}
                    </button>
                </div>
            </div>

            <!-- 任務列表 -->
            <div class="task-list">
                <h4>📝 任務列表 ({{ filteredTasks.length }} 項)</h4>
                <div v-if="filteredTasks.length === 0" class="empty-state">
                    <div class="empty-icon">📭</div>
                    <div class="empty-text">暫無符合條件的任務</div>
                </div>
                <TaskItem v-for="task in filteredTasks" :key="task.id" :task="task"
                    @toggle-complete="handleToggleComplete" @delete-task="handleDeleteTask"
                    @edit-task="handleEditTask" />
            </div>

            <!-- 任務詳情模態框 -->
            <TaskModal v-if="showModal" :task="selectedTask" @close="closeModal" @save="handleSaveTask" />
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import TaskForm from './components/TaskForm.vue'
import TaskItem from './components/TaskItem.vue'
import TaskModal from './components/TaskModal.vue'

// 響應式數據
const tasks = ref([
    {
        id: 1,
        title: '完成 Vue 專案',
        description: '建立一個完整的 Vue 3 應用程式',
        priority: 'high',
        completed: false,
        createdAt: new Date('2024-01-01'),
        dueDate: new Date('2024-01-15')
    },
    {
        id: 2,
        title: '學習 TypeScript',
        description: '掌握 TypeScript 的基本語法和進階特性',
        priority: 'medium',
        completed: true,
        createdAt: new Date('2024-01-02'),
        dueDate: new Date('2024-01-10')
    },
    {
        id: 3,
        title: '閱讀技術文檔',
        description: '閱讀 Vue 3 官方文檔',
        priority: 'low',
        completed: false,
        createdAt: new Date('2024-01-03'),
        dueDate: new Date('2024-01-20')
    }
])

const currentFilter = ref('all')
const showModal = ref(false)
const selectedTask = ref(null)

// 篩選選項
const filters = [
    { value: 'all', label: '全部任務' },
    { value: 'completed', label: '已完成' },
    { value: 'pending', label: '待完成' },
    { value: 'high', label: '高優先級' },
    { value: 'medium', label: '中優先級' },
    { value: 'low', label: '低優先級' }
]

// 1. completedCount (computed) - 計算已完成任務數量
const completedCount = computed(() => {
    return tasks.value.filter(task => task.completed).length
})

// 2. pendingCount (computed) - 計算待完成任務數量
const pendingCount = computed(() => {
    return tasks.value.filter(task => !task.completed).length
})

// 3. completionRate (computed) - 計算任務完成率百分比
const completionRate = computed(() => {
    if (tasks.value.length === 0) return 0
    return Math.round((completedCount.value / tasks.value.length) * 100)
})

// 4. filteredTasks (computed) - 根據篩選條件過濾任務
const filteredTasks = computed(() => {
    switch (currentFilter.value) {
        case 'all':
            return tasks.value
        case 'completed':
            return tasks.value.filter(task => task.completed)
        case 'pending':
            return tasks.value.filter(task => !task.completed)
        case 'high':
        case 'medium':
        case 'low':
            return tasks.value.filter(task => task.priority === currentFilter.value)
        default:
            return tasks.value
    }
})

// 5. handleAddTask(newTask) - 處理新增任務事件
const handleAddTask = (newTask) => {
    const task = {
        id: Date.now(),
        ...newTask,
        completed: false,
        createdAt: new Date()
    }
    tasks.value.push(task)
}

// 6. handleToggleComplete(taskId) - 切換任務完成狀態
const handleToggleComplete = (taskId) => {
    const taskIndex = tasks.value.findIndex(task => task.id === taskId)
    if (taskIndex !== -1) {
        tasks.value[taskIndex].completed = !tasks.value[taskIndex].completed
    }
}

// 處理刪除任務
const handleDeleteTask = (taskId) => {
    const taskIndex = tasks.value.findIndex(task => task.id === taskId)
    if (taskIndex !== -1) {
        tasks.value.splice(taskIndex, 1)
    }
}

// 處理編輯任務
const handleEditTask = (task) => {
    selectedTask.value = { ...task }
    showModal.value = true
}

// 處理保存任務
const handleSaveTask = (updatedTask) => {
    const taskIndex = tasks.value.findIndex(task => task.id === updatedTask.id)
    if (taskIndex !== -1) {
        tasks.value[taskIndex] = updatedTask
    }
    closeModal()
}

// 關閉模態框
const closeModal = () => {
    showModal.value = false
    selectedTask.value = null
}
</script>

<style scoped>
.self-challenge-solution {
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.route-info {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 8px 16px;
    border-radius: 20px;
    font-size: 14px;
    display: inline-block;
    margin-bottom: 20px;
}

.task-manager {
    display: grid;
    gap: 20px;
}

.stats-panel {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 15px;
    margin-bottom: 20px;
}

.stat-card {
    background: white;
    padding: 20px;
    border-radius: 15px;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
    border: 1px solid #e1e5e9;
    text-align: center;
    transition: transform 0.3s ease;
}

.stat-card:hover {
    transform: translateY(-5px);
}

.stat-value {
    font-size: 2.5rem;
    font-weight: bold;
    color: #2c3e50;
    margin-bottom: 5px;
}

.stat-label {
    color: #7f8c8d;
    font-size: 0.9rem;
}

.filter-panel {
    background: white;
    padding: 20px;
    border-radius: 15px;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
    border: 1px solid #e1e5e9;
}

.filter-panel h4 {
    color: #2c3e50;
    margin-bottom: 15px;
    text-align: center;
}

.filter-buttons {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    justify-content: center;
}

.filter-btn {
    padding: 10px 20px;
    border: 2px solid #e1e5e9;
    background: white;
    border-radius: 25px;
    cursor: pointer;
    transition: all 0.3s ease;
    font-weight: 500;
}

.filter-btn:hover {
    border-color: #3498db;
    transform: translateY(-2px);
}

.filter-btn.active {
    background: #3498db;
    color: white;
    border-color: #3498db;
}

.task-list {
    background: white;
    padding: 20px;
    border-radius: 15px;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
    border: 1px solid #e1e5e9;
}

.task-list h4 {
    color: #2c3e50;
    margin-bottom: 20px;
    text-align: center;
}

.empty-state {
    text-align: center;
    padding: 40px;
    color: #7f8c8d;
}

.empty-icon {
    font-size: 4rem;
    margin-bottom: 15px;
}

.empty-text {
    font-size: 1.1rem;
    font-style: italic;
}

@media (max-width: 768px) {
    .stats-panel {
        grid-template-columns: repeat(2, 1fr);
    }

    .filter-buttons {
        flex-direction: column;
        align-items: center;
    }

    .filter-btn {
        width: 100%;
        max-width: 200px;
    }
}
</style>
