<template>
    <div class="solution-card" :class="[
        `card-${color}`,
        `card-size-${size}`,
        {
            'card-elevated': elevated,
            'card-interactive': interactive,
            'card-bordered': bordered,
            'card-loading': loading
        }
    ]">
        <!-- 載入狀態 -->
        <div v-if="loading" class="loading-overlay">
            <div class="loading-spinner"></div>
            <span class="loading-text">載入中...</span>
        </div>

        <!-- 卡片標題區域 -->
        <div v-if="$slots.header || title || subtitle" class="card-header">
            <slot name="header">
                <div class="header-content">
                    <div class="header-main">
                        <h4 v-if="title" class="card-title">{{ title }}</h4>
                        <p v-if="subtitle" class="card-subtitle">{{ subtitle }}</p>
                    </div>

                    <!-- 右上角操作按鈕 -->
                    <div v-if="$slots.actions" class="header-actions">
                        <slot name="actions"></slot>
                    </div>
                </div>
            </slot>
        </div>

        <!-- 圖片區域 -->
        <div v-if="$slots.image || image" class="card-image">
            <slot name="image">
                <img :src="image" :alt="imageAlt" class="image" />
            </slot>
        </div>

        <!-- 主要內容區域 -->
        <div class="card-body">
            <slot>
                <div class="default-content">
                    <p>這是一個功能豐富的卡片組件</p>
                    <p>請使用插槽自定義內容</p>
                </div>
            </slot>
        </div>

        <!-- 標籤區域 -->
        <div v-if="$slots.tags || (tags && tags.length > 0)" class="card-tags">
            <slot name="tags">
                <span v-for="tag in tags" :key="tag" class="tag" :class="`tag-${color}`">
                    {{ tag }}
                </span>
            </slot>
        </div>

        <!-- 統計/指標區域 -->
        <div v-if="$slots.stats" class="card-stats">
            <slot name="stats"></slot>
        </div>

        <!-- 頁尾區域 -->
        <div v-if="$slots.footer" class="card-footer">
            <slot name="footer"></slot>
        </div>

        <!-- 展開內容區域 -->
        <transition name="expand">
            <div v-if="expanded && $slots.expanded" class="card-expanded">
                <slot name="expanded"></slot>
            </div>
        </transition>

        <!-- 展開/收合按鈕 -->
        <button v-if="expandable" @click="toggleExpanded" class="expand-toggle" :class="{ expanded }"
            :title="expanded ? '收合' : '展開'">
            <span class="expand-icon">{{ expanded ? '▲' : '▼' }}</span>
        </button>
    </div>
</template>

<script setup>
import { ref } from 'vue'

// 定義 props
// eslint-disable-next-line no-unused-vars
const props = defineProps({
    title: {
        type: String,
        default: ''
    },
    subtitle: {
        type: String,
        default: ''
    },
    color: {
        type: String,
        default: 'default',
        validator: (value) => {
            return ['default', 'primary', 'secondary', 'success', 'warning', 'danger', 'info'].includes(value)
        }
    },
    size: {
        type: String,
        default: 'medium',
        validator: (value) => {
            return ['small', 'medium', 'large'].includes(value)
        }
    },
    elevated: {
        type: Boolean,
        default: false
    },
    interactive: {
        type: Boolean,
        default: false
    },
    bordered: {
        type: Boolean,
        default: true
    },
    loading: {
        type: Boolean,
        default: false
    },
    expandable: {
        type: Boolean,
        default: false
    },
    image: {
        type: String,
        default: ''
    },
    imageAlt: {
        type: String,
        default: 'Card image'
    },
    tags: {
        type: Array,
        default: () => []
    }
})

// 定義 emit 事件
const emit = defineEmits(['click', 'expand', 'collapse'])

// 本地狀態
const expanded = ref(false)

// 方法
const toggleExpanded = () => {
    expanded.value = !expanded.value
    emit(expanded.value ? 'expand' : 'collapse')
}
</script>

<style scoped>
.solution-card {
    position: relative;
    background: white;
    border-radius: 12px;
    overflow: hidden;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    cursor: default;
}

/* 大小變體 */
.card-size-small {
    padding: 1rem;
}

.card-size-medium {
    padding: 1.5rem;
}

.card-size-large {
    padding: 2rem;
}

/* 邊框樣式 */
.card-bordered {
    border: 2px solid #e9ecef;
}

/* 陰影效果 */
.solution-card {
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.card-elevated {
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.15);
}

/* 互動效果 */
.card-interactive {
    cursor: pointer;
}

.card-interactive:hover {
    transform: translateY(-4px);
    box-shadow: 0 12px 40px rgba(0, 0, 0, 0.2);
}

/* 顏色主題 */
.card-default {
    border-color: #e9ecef;
}

.card-primary {
    border-color: #007bff;
}

.card-primary .card-header {
    background: linear-gradient(135deg, #007bff 0%, #0056b3 100%);
    color: white;
}

.card-secondary {
    border-color: #6c757d;
}

.card-secondary .card-header {
    background: linear-gradient(135deg, #6c757d 0%, #545b62 100%);
    color: white;
}

.card-success {
    border-color: #28a745;
}

.card-success .card-header {
    background: linear-gradient(135deg, #28a745 0%, #1e7e34 100%);
    color: white;
}

.card-warning {
    border-color: #ffc107;
}

.card-warning .card-header {
    background: linear-gradient(135deg, #ffc107 0%, #e0a800 100%);
    color: #212529;
}

.card-danger {
    border-color: #dc3545;
}

.card-danger .card-header {
    background: linear-gradient(135deg, #dc3545 0%, #c82333 100%);
    color: white;
}

.card-info {
    border-color: #17a2b8;
}

.card-info .card-header {
    background: linear-gradient(135deg, #17a2b8 0%, #138496 100%);
    color: white;
}

/* 載入狀態 */
.loading-overlay {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(255, 255, 255, 0.9);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    z-index: 10;
}

.loading-spinner {
    width: 40px;
    height: 40px;
    border: 4px solid #e9ecef;
    border-top: 4px solid #007bff;
    border-radius: 50%;
    animation: spin 1s linear infinite;
}

.loading-text {
    margin-top: 1rem;
    color: #6c757d;
    font-size: 0.875rem;
}

@keyframes spin {
    0% {
        transform: rotate(0deg);
    }

    100% {
        transform: rotate(360deg);
    }
}

/* 卡片區域 */
.card-header {
    margin: -1.5rem -1.5rem 1.5rem -1.5rem;
    padding: 1.5rem;
    background: #f8f9fa;
    border-bottom: 1px solid #e9ecef;
}

.header-content {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    gap: 1rem;
}

.header-main {
    flex: 1;
}

.card-title {
    margin: 0 0 0.5rem 0;
    font-size: 1.25rem;
    font-weight: 600;
    line-height: 1.3;
}

.card-subtitle {
    margin: 0;
    font-size: 0.875rem;
    opacity: 0.8;
    line-height: 1.4;
}

.header-actions {
    display: flex;
    gap: 0.5rem;
}

.card-image {
    margin: -1.5rem -1.5rem 1.5rem -1.5rem;
}

.image {
    width: 100%;
    height: 200px;
    object-fit: cover;
    display: block;
}

.card-body {
    flex: 1;
}

.default-content {
    text-align: center;
    color: #6c757d;
    font-style: italic;
}

.card-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
    margin-top: 1rem;
}

.tag {
    padding: 0.25rem 0.75rem;
    border-radius: 20px;
    font-size: 0.75rem;
    font-weight: 500;
    background: #e9ecef;
    color: #495057;
    border: 1px solid #dee2e6;
}

.tag-primary {
    background: #e3f2fd;
    color: #1976d2;
    border-color: #bbdefb;
}

.tag-success {
    background: #e8f5e8;
    color: #2e7d32;
    border-color: #c8e6c9;
}

.tag-warning {
    background: #fff8e1;
    color: #f57c00;
    border-color: #ffecb3;
}

.tag-danger {
    background: #ffebee;
    color: #c62828;
    border-color: #ffcdd2;
}

.card-stats {
    margin-top: 1rem;
    padding: 1rem;
    background: #f8f9fa;
    border-radius: 8px;
}

.card-footer {
    margin: 1.5rem -1.5rem -1.5rem -1.5rem;
    padding: 1rem 1.5rem;
    background: #f8f9fa;
    border-top: 1px solid #e9ecef;
}

/* 展開功能 */
.card-expanded {
    margin-top: 1rem;
    padding-top: 1rem;
    border-top: 1px solid #e9ecef;
}

.expand-toggle {
    position: absolute;
    bottom: 0.5rem;
    right: 0.5rem;
    width: 32px;
    height: 32px;
    border: none;
    border-radius: 50%;
    background: #007bff;
    color: white;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.3s ease;
    box-shadow: 0 2px 8px rgba(0, 123, 255, 0.3);
}

.expand-toggle:hover {
    background: #0056b3;
    transform: scale(1.1);
}

.expand-icon {
    font-size: 0.75rem;
    transition: transform 0.3s ease;
}

.expand-toggle.expanded .expand-icon {
    transform: rotate(180deg);
}

/* 展開動畫 */
.expand-enter-active,
.expand-leave-active {
    transition: all 0.3s ease;
    overflow: hidden;
}

.expand-enter-from,
.expand-leave-to {
    opacity: 0;
    max-height: 0;
    padding-top: 0;
    margin-top: 0;
}

.expand-enter-to,
.expand-leave-from {
    opacity: 1;
    max-height: 500px;
}

/* 響應式設計 */
@media (max-width: 768px) {
    .card-size-medium {
        padding: 1rem;
    }

    .card-size-large {
        padding: 1.5rem;
    }

    .card-header {
        margin: -1rem -1rem 1rem -1rem;
        padding: 1rem;
    }

    .card-image {
        margin: -1rem -1rem 1rem -1rem;
    }

    .image {
        height: 150px;
    }

    .card-footer {
        margin: 1rem -1rem -1rem -1rem;
        padding: 1rem;
    }

    .header-content {
        flex-direction: column;
        gap: 0.5rem;
    }

    .header-actions {
        width: 100%;
        justify-content: flex-end;
    }

    .card-tags {
        gap: 0.25rem;
    }

    .tag {
        font-size: 0.7rem;
        padding: 0.2rem 0.5rem;
    }
}
</style>
