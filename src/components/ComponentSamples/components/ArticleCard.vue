<template>
    <div class="article-card">
        <div class="card-header">
            <h4 class="article-title">{{ article.title }}</h4>
            <div class="article-meta">
                <span class="author">👤 {{ article.author }}</span>
                <span class="date">📅 {{ formatDate(article.createdAt) }}</span>
            </div>
        </div>

        <div class="card-body">
            <p class="article-content">{{ article.content }}</p>
        </div>

        <div class="card-footer">
            <div class="article-stats">
                <div class="stat-item">
                    <button @click="handleLike" class="like-btn" :class="{ liked: isLiked }">
                        {{ isLiked ? '❤️' : '🤍' }} {{ article.likes }}
                    </button>
                </div>
                <div class="stat-item">
                    <span class="read-time">⏱️ {{ readTime }} 分鐘閱讀</span>
                </div>
            </div>

            <div class="card-actions">
                <!-- 默認插槽 - 自定義操作按鈕 -->
                <slot name="actions">
                    <button class="action-btn edit-btn" @click="editArticle">
                        ✏️ 編輯
                    </button>
                </slot>

                <button @click="handleDelete" class="action-btn delete-btn" @mouseover="showDeleteConfirm = true"
                    @mouseleave="showDeleteConfirm = false">
                    {{ showDeleteConfirm ? '確認刪除?' : '🗑️ 刪除' }}
                </button>
            </div>
        </div>

        <!-- 文章詳情展開 -->
        <div v-if="showDetails" class="article-details">
            <div class="details-header">
                <h5>📊 文章詳情</h5>
                <button @click="showDetails = false" class="close-btn">✕</button>
            </div>
            <div class="details-content">
                <div class="detail-item">
                    <span class="detail-label">字數:</span>
                    <span class="detail-value">{{ article.content.length }} 字</span>
                </div>
                <div class="detail-item">
                    <span class="detail-label">創建時間:</span>
                    <span class="detail-value">{{ article.createdAt.toLocaleString() }}</span>
                </div>
                <div class="detail-item">
                    <span class="detail-label">點讚率:</span>
                    <span class="detail-value">{{ likeRate }}%</span>
                </div>
            </div>
        </div>

        <div class="card-toggle">
            <button @click="toggleDetails" class="toggle-btn">
                {{ showDetails ? '收起詳情 ▲' : '展開詳情 ▼' }}
            </button>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

// 定義 Props
const props = defineProps({
    article: {
        type: Object,
        required: true,
        validator: (value) => {
            return value && value.id && value.title && value.content && value.author
        }
    },
    showActions: {
        type: Boolean,
        default: true
    }
})

// 定義事件發射
const emit = defineEmits(['like', 'delete', 'edit', 'task-completed'])

// 響應式數據
const isLiked = ref(false)
const showDetails = ref(false)
const showDeleteConfirm = ref(false)

// 計算屬性
const readTime = computed(() => {
    const wordsPerMinute = 200
    const wordCount = props.article.content.length
    return Math.max(1, Math.ceil(wordCount / wordsPerMinute))
})

const likeRate = computed(() => {
    // 模擬點讚率計算
    const baseRate = Math.min(95, props.article.likes * 2.5)
    return Math.round(baseRate)
})

// 方法
const formatDate = (date) => {
    return date.toLocaleDateString('zh-TW', {
        year: 'numeric',
        month: 'short',
        day: 'numeric'
    })
}

const handleLike = () => {
    isLiked.value = !isLiked.value
    emit('like', props.article.id)
    emit('task-completed', 'eventEmit')
}

const handleDelete = () => {
    if (confirm(`確定要刪除文章「${props.article.title}」嗎？`)) {
        emit('delete', props.article.id)
        emit('task-completed', 'eventEmit')
    }
}

const editArticle = () => {
    alert(`編輯文章: ${props.article.title}`)
    emit('edit', props.article.id)
}

const toggleDetails = () => {
    showDetails.value = !showDetails.value
}

// 組件掛載時標記任務完成
onMounted(() => {
    emit('task-completed', 'propsUsage')
    emit('task-completed', 'slotUsage')
})
</script>

<style scoped>
.article-card {
    background: white;
    border-radius: 12px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    overflow: hidden;
    transition: all 0.3s ease;
    border: 1px solid #e9ecef;
}

.article-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

.card-header {
    padding: 20px 20px 15px 20px;
    border-bottom: 1px solid #f1f3f4;
}

.article-title {
    margin: 0 0 10px 0;
    color: #2c3e50;
    font-size: 1.2em;
    font-weight: 600;
    line-height: 1.4;
}

.article-meta {
    display: flex;
    gap: 15px;
    font-size: 0.85em;
    color: #6c757d;
}

.card-body {
    padding: 15px 20px;
}

.article-content {
    margin: 0;
    color: #495057;
    line-height: 1.6;
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
    overflow: hidden;
}

.card-footer {
    padding: 15px 20px;
    background: #f8f9fa;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.article-stats {
    display: flex;
    gap: 15px;
    align-items: center;
}

.stat-item {
    display: flex;
    align-items: center;
}

.like-btn {
    background: none;
    border: none;
    cursor: pointer;
    font-size: 14px;
    padding: 5px 10px;
    border-radius: 20px;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    gap: 5px;
}

.like-btn:hover {
    background: #f8f9fa;
}

.like-btn.liked {
    color: #e74c3c;
    background: #ffeaea;
}

.read-time {
    font-size: 0.85em;
    color: #6c757d;
}

.card-actions {
    display: flex;
    gap: 10px;
}

.action-btn {
    padding: 8px 16px;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-size: 13px;
    font-weight: 500;
    transition: all 0.3s ease;
}

.edit-btn {
    background: #007bff;
    color: white;
}

.edit-btn:hover {
    background: #0056b3;
    transform: translateY(-1px);
}

.delete-btn {
    background: #dc3545;
    color: white;
}

.delete-btn:hover {
    background: #c82333;
    transform: translateY(-1px);
}

.article-details {
    padding: 20px;
    background: #f8f9fa;
    border-top: 1px solid #dee2e6;
}

.details-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 15px;
}

.details-header h5 {
    margin: 0;
    color: #495057;
}

.close-btn {
    background: none;
    border: none;
    font-size: 18px;
    cursor: pointer;
    color: #6c757d;
    padding: 0;
    width: 24px;
    height: 24px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
}

.close-btn:hover {
    background: #e9ecef;
    color: #495057;
}

.details-content {
    display: grid;
    gap: 10px;
}

.detail-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 8px 0;
}

.detail-label {
    font-weight: 600;
    color: #495057;
}

.detail-value {
    color: #6c757d;
}

.card-toggle {
    padding: 10px 20px;
    background: #f8f9fa;
    border-top: 1px solid #dee2e6;
    text-align: center;
}

.toggle-btn {
    background: none;
    border: none;
    color: #007bff;
    cursor: pointer;
    font-size: 13px;
    padding: 5px 10px;
    border-radius: 4px;
    transition: all 0.3s ease;
}

.toggle-btn:hover {
    background: #e3f2fd;
    color: #0056b3;
}

@media (max-width: 768px) {
    .card-footer {
        flex-direction: column;
        gap: 15px;
        align-items: stretch;
    }

    .article-stats {
        justify-content: center;
    }

    .card-actions {
        justify-content: center;
    }

    .article-meta {
        flex-direction: column;
        gap: 5px;
    }
}
</style>
