<template>
    <div class="stats-panel">
        <div class="panel-header">
            <h4>📊 博客統計面板</h4>
            <p>實時數據統計與分析</p>
        </div>

        <div class="stats-grid">
            <div class="stat-card total-articles">
                <div class="stat-icon">📝</div>
                <div class="stat-content">
                    <div class="stat-number">{{ totalArticles }}</div>
                    <div class="stat-label">總文章數</div>
                    <div class="stat-trend">
                        <span class="trend-indicator positive">↗️ +{{ Math.floor(totalArticles * 0.15) }}</span>
                        <span class="trend-text">本月新增</span>
                    </div>
                </div>
            </div>

            <div class="stat-card total-likes">
                <div class="stat-icon">❤️</div>
                <div class="stat-content">
                    <div class="stat-number">{{ totalLikes }}</div>
                    <div class="stat-label">總點讚數</div>
                    <div class="stat-trend">
                        <span class="trend-indicator positive">↗️ +{{ Math.floor(totalLikes * 0.25) }}</span>
                        <span class="trend-text">本週新增</span>
                    </div>
                </div>
            </div>

            <div class="stat-card avg-likes">
                <div class="stat-icon">📈</div>
                <div class="stat-content">
                    <div class="stat-number">{{ averageLikes }}</div>
                    <div class="stat-label">平均點讚</div>
                    <div class="stat-trend">
                        <span class="trend-indicator" :class="trendClass">
                            {{ trendIcon }} {{ trendValue }}
                        </span>
                        <span class="trend-text">較上月</span>
                    </div>
                </div>
            </div>

            <div class="stat-card engagement">
                <div class="stat-icon">🎯</div>
                <div class="stat-content">
                    <div class="stat-number">{{ engagementRate }}%</div>
                    <div class="stat-label">參與度</div>
                    <div class="stat-trend">
                        <span class="trend-indicator positive">↗️ +2.3%</span>
                        <span class="trend-text">持續上升</span>
                    </div>
                </div>
            </div>
        </div>

        <!-- 最受歡迎文章 -->
        <div v-if="mostLikedArticle" class="popular-article">
            <h5>🏆 最受歡迎文章</h5>
            <div class="popular-card">
                <div class="popular-content">
                    <h6>{{ mostLikedArticle.title }}</h6>
                    <p>{{ mostLikedArticle.content.substring(0, 100) }}...</p>
                    <div class="popular-meta">
                        <span class="author">👤 {{ mostLikedArticle.author }}</span>
                        <span class="likes">❤️ {{ mostLikedArticle.likes }} 點讚</span>
                        <span class="date">📅 {{ formatDate(mostLikedArticle.createdAt) }}</span>
                    </div>
                </div>
                <div class="popular-badge">
                    <div class="badge-icon">👑</div>
                    <div class="badge-text">熱門</div>
                </div>
            </div>
        </div>

        <!-- 數據圖表模擬 -->
        <div class="chart-section">
            <h5>📊 點讚趨勢圖</h5>
            <div class="chart-container">
                <div class="chart-bars">
                    <div v-for="(bar, index) in chartData" :key="index" class="chart-bar"
                        :style="{ height: bar.height + '%' }" :title="`${bar.label}: ${bar.value} 點讚`">
                        <div class="bar-value">{{ bar.value }}</div>
                    </div>
                </div>
                <div class="chart-labels">
                    <span v-for="(bar, index) in chartData" :key="index" class="chart-label">
                        {{ bar.label }}
                    </span>
                </div>
            </div>
        </div>

        <!-- 快速操作 -->
        <div class="quick-actions">
            <h5>⚡ 快速操作</h5>
            <div class="action-buttons">
                <button @click="refreshStats" class="action-btn refresh-btn">
                    🔄 刷新數據
                </button>
                <button @click="exportStats" class="action-btn export-btn">
                    📤 導出報告
                </button>
                <button @click="viewDetails" class="action-btn details-btn">
                    📋 詳細分析
                </button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { computed, onMounted } from 'vue'

// 定義 Props
const props = defineProps({
    totalArticles: {
        type: Number,
        default: 0
    },
    totalLikes: {
        type: Number,
        default: 0
    },
    mostLikedArticle: {
        type: Object,
        default: null
    }
})

// 定義事件發射
const emit = defineEmits(['task-completed'])

// 計算屬性
const averageLikes = computed(() => {
    if (props.totalArticles === 0) return 0
    return Math.round(props.totalLikes / props.totalArticles)
})

const engagementRate = computed(() => {
    // 模擬參與度計算
    const baseRate = Math.min(100, (props.totalLikes / Math.max(1, props.totalArticles)) * 10)
    return Math.round(baseRate)
})

const trendValue = computed(() => {
    const change = Math.floor(Math.random() * 10) - 5
    return Math.abs(change)
})

const trendClass = computed(() => {
    return Math.random() > 0.5 ? 'positive' : 'negative'
})

const trendIcon = computed(() => {
    return trendClass.value === 'positive' ? '↗️' : '↘️'
})

const chartData = computed(() => {
    const days = ['週一', '週二', '週三', '週四', '週五', '週六', '週日']
    return days.map(day => {
        const value = Math.floor(Math.random() * 50) + 10
        return {
            label: day,
            value: value,
            height: (value / 60) * 100
        }
    })
})

// 方法
const formatDate = (date) => {
    return date.toLocaleDateString('zh-TW', {
        month: 'short',
        day: 'numeric'
    })
}

const refreshStats = () => {
    alert('數據已刷新！')
}

const exportStats = () => {
    alert('統計報告已導出！')
}

const viewDetails = () => {
    alert('查看詳細分析報告')
}

// 組件掛載時標記任務完成
onMounted(() => {
    emit('task-completed', 'propsUsage')
    emit('task-completed', 'componentComposition')
})
</script>

<style scoped>
.stats-panel {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 25px;
    border-radius: 15px;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
}

.panel-header {
    text-align: center;
    margin-bottom: 25px;
}

.panel-header h4 {
    margin: 0 0 8px 0;
    font-size: 1.4em;
    font-weight: 600;
}

.panel-header p {
    margin: 0;
    opacity: 0.9;
    font-size: 0.9em;
}

.stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 20px;
    margin-bottom: 30px;
}

.stat-card {
    background: rgba(255, 255, 255, 0.15);
    backdrop-filter: blur(10px);
    border-radius: 12px;
    padding: 20px;
    display: flex;
    align-items: center;
    gap: 15px;
    transition: all 0.3s ease;
    border: 1px solid rgba(255, 255, 255, 0.2);
}

.stat-card:hover {
    transform: translateY(-4px);
    background: rgba(255, 255, 255, 0.2);
}

.stat-icon {
    font-size: 2.5em;
    opacity: 0.9;
}

.stat-content {
    flex: 1;
}

.stat-number {
    font-size: 2em;
    font-weight: 700;
    margin-bottom: 5px;
}

.stat-label {
    font-size: 0.9em;
    opacity: 0.9;
    margin-bottom: 8px;
}

.stat-trend {
    display: flex;
    align-items: center;
    gap: 8px;
    font-size: 0.8em;
}

.trend-indicator {
    padding: 2px 6px;
    border-radius: 12px;
    font-weight: 600;
}

.trend-indicator.positive {
    background: rgba(40, 167, 69, 0.3);
    color: #90ee90;
}

.trend-indicator.negative {
    background: rgba(220, 53, 69, 0.3);
    color: #ffb3b3;
}

.trend-text {
    opacity: 0.8;
}

.popular-article {
    background: rgba(255, 255, 255, 0.1);
    border-radius: 12px;
    padding: 20px;
    margin-bottom: 25px;
}

.popular-article h5 {
    margin: 0 0 15px 0;
    font-size: 1.1em;
}

.popular-card {
    background: rgba(255, 255, 255, 0.1);
    border-radius: 10px;
    padding: 15px;
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    gap: 15px;
}

.popular-content {
    flex: 1;
}

.popular-content h6 {
    margin: 0 0 8px 0;
    font-size: 1em;
    font-weight: 600;
}

.popular-content p {
    margin: 0 0 10px 0;
    opacity: 0.9;
    font-size: 0.85em;
    line-height: 1.4;
}

.popular-meta {
    display: flex;
    gap: 15px;
    font-size: 0.8em;
    opacity: 0.8;
}

.popular-badge {
    text-align: center;
    background: rgba(255, 215, 0, 0.3);
    border-radius: 8px;
    padding: 10px;
    min-width: 60px;
}

.badge-icon {
    font-size: 1.5em;
    margin-bottom: 4px;
}

.badge-text {
    font-size: 0.8em;
    font-weight: 600;
}

.chart-section {
    background: rgba(255, 255, 255, 0.1);
    border-radius: 12px;
    padding: 20px;
    margin-bottom: 25px;
}

.chart-section h5 {
    margin: 0 0 15px 0;
    font-size: 1.1em;
}

.chart-container {
    height: 150px;
    display: flex;
    flex-direction: column;
}

.chart-bars {
    flex: 1;
    display: flex;
    align-items: end;
    gap: 8px;
    padding-bottom: 10px;
}

.chart-bar {
    flex: 1;
    background: linear-gradient(to top, rgba(255, 255, 255, 0.6), rgba(255, 255, 255, 0.3));
    border-radius: 4px 4px 0 0;
    position: relative;
    min-height: 20px;
    transition: all 0.3s ease;
    cursor: pointer;
}

.chart-bar:hover {
    background: linear-gradient(to top, rgba(255, 255, 255, 0.8), rgba(255, 255, 255, 0.5));
}

.bar-value {
    position: absolute;
    top: -20px;
    left: 50%;
    transform: translateX(-50%);
    font-size: 0.7em;
    font-weight: 600;
    opacity: 0;
    transition: opacity 0.3s ease;
}

.chart-bar:hover .bar-value {
    opacity: 1;
}

.chart-labels {
    display: flex;
    gap: 8px;
    padding-top: 10px;
    border-top: 1px solid rgba(255, 255, 255, 0.2);
}

.chart-label {
    flex: 1;
    text-align: center;
    font-size: 0.8em;
    opacity: 0.8;
}

.quick-actions {
    background: rgba(255, 255, 255, 0.1);
    border-radius: 12px;
    padding: 20px;
}

.quick-actions h5 {
    margin: 0 0 15px 0;
    font-size: 1.1em;
}

.action-buttons {
    display: flex;
    gap: 12px;
    flex-wrap: wrap;
}

.action-btn {
    padding: 10px 16px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-size: 0.85em;
    font-weight: 600;
    transition: all 0.3s ease;
    background: rgba(255, 255, 255, 0.2);
    color: white;
    border: 1px solid rgba(255, 255, 255, 0.3);
}

.action-btn:hover {
    background: rgba(255, 255, 255, 0.3);
    transform: translateY(-2px);
}

@media (max-width: 768px) {
    .stats-grid {
        grid-template-columns: 1fr;
    }

    .popular-card {
        flex-direction: column;
    }

    .popular-meta {
        flex-direction: column;
        gap: 5px;
    }

    .action-buttons {
        flex-direction: column;
    }
}
</style>
