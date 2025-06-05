<template>
    <div class="stats-card" :class="`color-${color}`">
        <div class="card-content">
            <!-- 圖標區域 -->
            <div class="card-icon">
                <span class="icon">{{ /* TODO: 顯示圖標 */ }}</span>
            </div>

            <!-- 數據區域 -->
            <div class="card-data">
                <h3 class="card-value">{{ /* TODO: 顯示格式化後的值 */ }}</h3>
                <p class="card-title">{{ title }}</p>
            </div>

            <!-- 趨勢指示器（可選） -->
            <div v-if="trend" class="card-trend" :class="`trend-${trend}`">
                <span class="trend-icon">{{ /* TODO: 顯示趨勢圖標 */ }}</span>
                <span class="trend-text">{{ trendText }}</span>
            </div>
        </div>

        <!-- 進度條（可選） -->
        <div v-if="showProgress" class="card-progress">
            <div class="progress-bar" :style="{ /* TODO: 設置進度條寬度 */ }"></div>
        </div>
    </div>
</template>

<script setup>
import { computed } from 'vue'

// TODO: 定義組件接收的 props
// 提示：定義 title, value, color 等必要屬性
const props = defineProps({
    // TODO: 定義各種 props
    // 提示：title (String, required), value (String|Number, required), color (String, default: 'blue')
})

// TODO: 實現計算屬性
const formattedValue = computed(() => {
    // TODO: 格式化顯示值
    // 提示：如果是數字，使用 toLocaleString() 格式化
    return ''
})

const progressPercentage = computed(() => {
    // TODO: 計算進度百分比
    // 提示：(value / maxValue) * 100，但不超過 100
    return 0
})

// TODO: 實現圖標選擇方法
const getIcon = () => {
    // TODO: 根據顏色或標題返回對應圖標
    // 提示：可以根據標題關鍵字智能選擇圖標
    return '📊'
}

const getTrendIcon = () => {
    // TODO: 根據趨勢返回對應圖標
    // 提示：up: '📈', down: '📉', stable: '➡️'
    return ''
}
</script>

<style scoped>
.stats-card {
    background: white;
    border-radius: 15px;
    padding: 25px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
    transition: all 0.3s ease;
    position: relative;
    overflow: hidden;
    border-left: 5px solid;
}

.stats-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 30px rgba(0, 0, 0, 0.15);
}

/* 顏色主題 */
.stats-card.color-blue {
    border-left-color: #007bff;
}

.stats-card.color-green {
    border-left-color: #28a745;
}

.stats-card.color-orange {
    border-left-color: #fd7e14;
}

.stats-card.color-purple {
    border-left-color: #6f42c1;
}

.stats-card.color-red {
    border-left-color: #dc3545;
}

.card-content {
    display: flex;
    align-items: center;
    gap: 15px;
}

.card-icon {
    flex-shrink: 0;
    width: 50px;
    height: 50px;
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.5em;
    background: rgba(0, 123, 255, 0.1);
}

.color-blue .card-icon {
    background: rgba(0, 123, 255, 0.1);
}

.color-green .card-icon {
    background: rgba(40, 167, 69, 0.1);
}

.color-orange .card-icon {
    background: rgba(253, 126, 20, 0.1);
}

.color-purple .card-icon {
    background: rgba(111, 66, 193, 0.1);
}

.color-red .card-icon {
    background: rgba(220, 53, 69, 0.1);
}

.card-data {
    flex: 1;
    min-width: 0;
}

.card-value {
    margin: 0 0 5px 0;
    font-size: 2.2em;
    font-weight: 700;
    color: #333;
    line-height: 1;
}

.card-title {
    margin: 0;
    color: #666;
    font-size: 0.95em;
    font-weight: 500;
}

.card-trend {
    flex-shrink: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 4px;
}

.trend-icon {
    font-size: 1.2em;
}

.trend-text {
    font-size: 0.8em;
    font-weight: 600;
}

.trend-up {
    color: #28a745;
}

.trend-down {
    color: #dc3545;
}

.trend-stable {
    color: #6c757d;
}

.card-progress {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    height: 4px;
    background: rgba(0, 0, 0, 0.1);
}

.progress-bar {
    height: 100%;
    background: linear-gradient(90deg, #007bff, #0056b3);
    transition: width 0.8s ease;
    border-radius: 0 0 15px 15px;
}

.color-green .progress-bar {
    background: linear-gradient(90deg, #28a745, #1e7e34);
}

.color-orange .progress-bar {
    background: linear-gradient(90deg, #fd7e14, #e8650e);
}

.color-purple .progress-bar {
    background: linear-gradient(90deg, #6f42c1, #59359a);
}

.color-red .progress-bar {
    background: linear-gradient(90deg, #dc3545, #c82333);
}

/* 響應式設計 */
@media (max-width: 768px) {
    .stats-card {
        padding: 20px;
    }

    .card-content {
        gap: 12px;
    }

    .card-icon {
        width: 40px;
        height: 40px;
        font-size: 1.2em;
    }

    .card-value {
        font-size: 1.8em;
    }

    .card-title {
        font-size: 0.9em;
    }

    .card-trend {
        display: none;
    }
}

@media (max-width: 480px) {
    .card-content {
        flex-direction: column;
        text-align: center;
        gap: 10px;
    }

    .card-data {
        order: -1;
    }
}
</style>
