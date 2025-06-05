<template>
    <div class="empty-state">
        <div class="empty-content">
            <!-- 圖標插槽 -->
            <div class="empty-icon">
                <!-- TODO: 使用具名插槽顯示圖標 -->
                <!-- 提示：<slot name="icon">預設圖標</slot> -->
                🗂️
            </div>

            <!-- 標題插槽 -->
            <h3 class="empty-title">
                <!-- TODO: 使用具名插槽顯示標題 -->
                暫無數據
            </h3>

            <!-- 描述插槽 -->
            <div class="empty-description">
                <!-- TODO: 使用具名插槽顯示描述 -->
                目前沒有任何內容
            </div>

            <!-- 操作按鈕插槽 -->
            <div class="empty-actions">
                <!-- TODO: 使用具名插槽顯示操作按鈕 -->

            </div>
        </div>
    </div>
</template>

<script setup>
// TODO: 這個組件主要用於展示插槽的使用
// 提示：EmptyState 組件通常不需要特殊的邏輯，主要是展示插槽內容
</script>

<style scoped>
.empty-state {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 60px 40px;
    text-align: center;
    background: #fafbfc;
    border-radius: 12px;
    border: 2px dashed #e1e5e9;
    min-height: 300px;
}

.empty-content {
    max-width: 400px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
}

.empty-icon {
    font-size: 4rem;
    opacity: 0.6;
    margin-bottom: 10px;
}

.empty-title {
    margin: 0;
    color: #424242;
    font-size: 1.5rem;
    font-weight: 600;
}

.empty-description {
    color: #757575;
    font-size: 1rem;
    line-height: 1.6;
    margin: 0;
}

.empty-actions {
    margin-top: 20px;
}

@media (max-width: 768px) {
    .empty-state {
        padding: 40px 20px;
        min-height: 250px;
    }

    .empty-icon {
        font-size: 3rem;
    }

    .empty-title {
        font-size: 1.3rem;
    }

    .empty-description {
        font-size: 0.9rem;
    }
}
</style>
