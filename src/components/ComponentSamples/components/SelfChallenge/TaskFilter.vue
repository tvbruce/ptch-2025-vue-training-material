<template>
    <div class="task-filter">
        <h4>🔍 任務篩選</h4>

        <div class="filter-controls">
            <!-- 快速篩選按鈕 -->
            <div class="filter-buttons">
                <!-- TODO: 實現篩選按鈕，使用 v-model 更新值 -->
                <button v-for="filter in filterOptions" :key="filter.value" class="filter-btn" @click="">
                    {{ filter.icon }} {{ filter.label }}
                </button>
            </div>

            <!-- 自定義篩選 -->
            <div class="custom-filters">
                <div class="filter-group">
                    <label>優先級篩選：</label>
                    <select class="filter-select">
                        <option value="">全部優先級</option>
                        <option value="high">高優先級</option>
                        <option value="medium">中優先級</option>
                        <option value="low">低優先級</option>
                    </select>
                </div>

                <div class="filter-group">
                    <label>分類篩選：</label>
                    <input type="text" class="filter-input" placeholder="輸入分類名稱" />
                </div>
            </div>

            <!-- 重置篩選 -->
            <div class="filter-actions">
                <button class="btn btn-reset" @click="">
                    🔄 重置篩選
                </button>
            </div>
        </div>

        <!-- 篩選狀態顯示 -->
        <!-- TODO: 根據篩選狀態決定是否顯示 -->
        <div class="filter-status">
            <span class="status-text">目前篩選：</span>
            <div class="active-filters">
                <!-- TODO: 顯示當前活躍的篩選條件 -->
                <span class="filter-tag">篩選條件</span>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// TODO: 定義 props 和 emits
// 提示：支援 v-model 需要定義 modelValue prop 和 update:modelValue emit
const props = defineProps({
    // TODO: 定義 modelValue prop
})

const emit = defineEmits([
    // TODO: 定義事件
    // 提示：'update:modelValue', 'filter-change'
])

// TODO: 定義篩選選項
const filterOptions = [
    // TODO: 定義篩選選項數組
    // 提示：{ value: 'all', label: '全部任務', icon: '📋' }
]

// TODO: 定義額外篩選條件
const priorityFilter = ref('')
const categoryFilter = ref('')

// TODO: 實現計算屬性
const hasActiveFilters = computed(() => {
    // TODO: 判斷是否有活躍的篩選條件
    return false
})

// TODO: 實現篩選變更方法
const handleFilterChange = (filterValue) => {
    // TODO: 更新 v-model 值並發射事件
    // 提示：使用 emit('update:modelValue', value) 更新 v-model
    console.log('篩選變更:', filterValue)
}

const handlePriorityChange = (event) => {
    // TODO: 處理優先級篩選變更
    console.log('優先級變更:', event.target.value)
}

const handleCategoryChange = (event) => {
    // TODO: 處理分類篩選變更
    console.log('分類變更:', event.target.value)
}

const resetFilters = () => {
    // TODO: 重置所有篩選條件
    console.log('重置篩選')
}

// 工具方法
const getCurrentFilterLabel = () => {
    // TODO: 根據當前篩選值返回對應標籤
    return '未知篩選'
}

const getPriorityLabel = (priority) => {
    // TODO: 根據優先級值返回中文標籤
    return priority
}
</script>

<style scoped>
.task-filter {
    background: white;
    border-radius: 12px;
    padding: 20px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    border: 1px solid #e9ecef;
}

.task-filter h4 {
    margin: 0 0 20px 0;
    color: #333;
    font-size: 1.2em;
    text-align: center;
}

.filter-controls {
    display: flex;
    flex-direction: column;
    gap: 20px;
}

.filter-buttons {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    justify-content: center;
}

.filter-btn {
    padding: 10px 16px;
    border: 2px solid #e9ecef;
    border-radius: 25px;
    background: white;
    cursor: pointer;
    font-size: 0.9em;
    font-weight: 500;
    transition: all 0.3s ease;
    color: #666;
}

.filter-btn:hover {
    border-color: #007bff;
    color: #007bff;
    transform: translateY(-2px);
}

.filter-btn.active {
    background: linear-gradient(135deg, #007bff, #0056b3);
    border-color: #007bff;
    color: white;
    box-shadow: 0 4px 15px rgba(0, 123, 255, 0.3);
}

.custom-filters {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 15px;
    padding: 15px;
    background: #f8f9fa;
    border-radius: 10px;
}

.filter-group {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

.filter-group label {
    font-weight: 600;
    color: #555;
    font-size: 0.9em;
}

.filter-select,
.filter-input {
    padding: 8px 12px;
    border: 1px solid #ddd;
    border-radius: 6px;
    font-size: 0.9em;
    transition: all 0.3s ease;
}

.filter-select:focus,
.filter-input:focus {
    outline: none;
    border-color: #007bff;
    box-shadow: 0 0 0 2px rgba(0, 123, 255, 0.1);
}

.filter-actions {
    display: flex;
    justify-content: center;
}

.btn {
    padding: 10px 20px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-size: 0.9em;
    font-weight: 600;
    transition: all 0.3s ease;
}

.btn-reset {
    background: #6c757d;
    color: white;
}

.btn-reset:hover {
    background: #545b62;
    transform: translateY(-2px);
}

.filter-status {
    margin-top: 20px;
    padding: 15px;
    background: #e7f3ff;
    border-radius: 10px;
    border-left: 4px solid #007bff;
}

.status-text {
    font-weight: 600;
    color: #333;
    margin-bottom: 10px;
    display: block;
}

.active-filters {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
}

.filter-tag {
    padding: 4px 12px;
    background: #007bff;
    color: white;
    border-radius: 15px;
    font-size: 0.8em;
    font-weight: 500;
}

@media (max-width: 768px) {
    .filter-buttons {
        justify-content: stretch;
    }

    .filter-btn {
        flex: 1;
        min-width: 120px;
    }

    .custom-filters {
        grid-template-columns: 1fr;
        gap: 15px;
    }

    .active-filters {
        justify-content: center;
    }
}
</style>
