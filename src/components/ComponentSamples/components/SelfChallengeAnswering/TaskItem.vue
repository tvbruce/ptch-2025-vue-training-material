<template>
    <div class="task-item" :class="{ completed: task.completed }">
        <!-- 🎯 任務：建立任務標題和優先級顯示 -->
        <div class="task-header">
            <h5 class="task-title">任務標題待顯示</h5>
            <span class="priority-badge">
                優先級待顯示
            </span>
        </div>

        <!-- 🎯 任務：建立任務描述顯示 -->
        <p class="task-description">任務描述待顯示</p>

        <!-- 🎯 任務：建立任務操作按鈕 -->
        <div class="task-actions">
            <button @click="handleToggleComplete" class="btn btn-toggle">
                標記完成
            </button>

            <button @click="handleDelete" class="btn btn-danger">
                刪除
            </button>
        </div>

        <!-- 開發提示區域 -->
        <div class="dev-hints">
            <h6>💡 實作提示：</h6>
            <ul>
                <li>使用 雙大括號task.title雙大括號 顯示任務標題</li>
                <li>使用 雙大括號task.description雙大括號 顯示任務描述</li>
                <li>使用 :class 根據 task.completed 添加樣式</li>
                <li>使用 :class="['priority-badge', task.priority]" 設定優先級樣式</li>
                <li>使用計算屬性轉換優先級為中文</li>
            </ul>
        </div>
    </div>
</template>

<script setup>
// 🎯 任務：導入需要的 Vue 函數
// 提示：import { computed } from 'vue'

// 🎯 任務：定義 props
// 提示：接收 task 物件作為 prop
// const props = defineProps({
//   task: {
//     type: Object,
//     required: true
//   }
// })

// 🎯 任務：定義 emit 事件
// 提示：定義切換完成和刪除事件
// const emit = defineEmits(['toggle-complete', 'delete-task'])

// 🎯 任務：實作優先級文字計算屬性
// 提示：使用 computed 將 'high', 'medium', 'low' 轉換為中文
// const priorityText = computed(() => {
//   const priorityMap = {
//     high: '高優先級',
//     medium: '中優先級',
//     low: '低優先級'
//   }
//   return priorityMap[props.task.priority] || '未知'
// })

// 🎯 任務：實作切換完成狀態處理
const handleToggleComplete = () => {
    // 請在這裡實作切換完成狀態邏輯
    // 發送 toggle-complete 事件給父組件，傳遞任務 ID
    console.log('🎯 待實作：切換完成狀態功能')
}

// 🎯 任務：實作刪除處理
const handleDelete = () => {
    // 請在這裡實作刪除邏輯
    // 可以加入確認對話框
    // 發送 delete-task 事件給父組件，傳遞任務 ID
    console.log('🎯 待實作：刪除任務功能')
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
    margin-bottom: 1rem;
}

.task-item:hover {
    border-color: #20c997;
    transform: translateY(-2px);
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
    background: #e9ecef;
    color: #495057;
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

.task-actions {
    display: flex;
    gap: 0.5rem;
    margin-bottom: 1rem;
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

.dev-hints {
    background: #fff3cd;
    border: 1px solid #ffeaa7;
    border-radius: 8px;
    padding: 1rem;
    margin-top: 1rem;
}

.dev-hints h6 {
    margin: 0 0 0.5rem 0;
    color: #856404;
    font-size: 0.9rem;
}

.dev-hints ul {
    margin: 0;
    padding-left: 1.2rem;
}

.dev-hints li {
    color: #856404;
    font-size: 0.8rem;
    margin-bottom: 0.25rem;
}

@media (max-width: 768px) {
    .task-header {
        flex-direction: column;
        gap: 0.5rem;
    }

    .task-actions {
        flex-direction: column;
    }
}
</style>
