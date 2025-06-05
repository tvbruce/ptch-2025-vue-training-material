<template>
    <div class="card" :class="[`card-${color}`, { 'card-shadow': shadow }]">
        <!-- 🎯 任務：實作 header 具名插槽 -->
        <div v-if="$slots.header || title" class="card-header">
            <slot name="header">
                <h4 class="card-title">{{ title }}</h4>
            </slot>
        </div>

        <!-- 🎯 任務：實作預設插槽 -->
        <div class="card-body">
            <slot>
                <p>這是預設內容，請使用插槽自定義內容</p>
            </slot>
        </div>

        <!-- 🎯 任務：實作 footer 具名插槽 -->
        <div v-if="$slots.footer" class="card-footer">
            <slot name="footer"></slot>
        </div>
    </div>
</template>

<script setup>
// 🎯 任務：定義 props
// 提示：title, color, shadow
// eslint-disable-next-line no-unused-vars
const props = defineProps({
    title: {
        type: String,
        default: ''
    },
    color: {
        type: String,
        default: 'default',
        validator: (value) => {
            return ['default', 'primary', 'success', 'warning', 'danger', 'info'].includes(value)
        }
    },
    shadow: {
        type: Boolean,
        default: true
    }
})
</script>

<style scoped>
.card {
    background: white;
    border-radius: 8px;
    overflow: hidden;
    transition: all 0.3s ease;
    border: 1px solid #e9ecef;
}

.card-shadow {
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.card:hover.card-shadow {
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
    transform: translateY(-2px);
}

.card-header {
    padding: 1.5rem 1.5rem 0 1.5rem;
    border-bottom: 1px solid #e9ecef;
    margin-bottom: 0;
}

.card-title {
    margin: 0 0 1rem 0;
    color: #495057;
    font-size: 1.2rem;
    font-weight: 600;
}

.card-body {
    padding: 1.5rem;
}

.card-footer {
    padding: 1rem 1.5rem;
    background: #f8f9fa;
    border-top: 1px solid #e9ecef;
}

/* 顏色主題 */
.card-default {
    border-color: #e9ecef;
}

.card-primary {
    border-color: #007bff;
}

.card-primary .card-header {
    background: #007bff;
    color: white;
    border-bottom-color: #0056b3;
}

.card-primary .card-title {
    color: white;
}

.card-success {
    border-color: #28a745;
}

.card-success .card-header {
    background: #28a745;
    color: white;
    border-bottom-color: #1e7e34;
}

.card-success .card-title {
    color: white;
}

.card-warning {
    border-color: #ffc107;
}

.card-warning .card-header {
    background: #ffc107;
    color: #212529;
    border-bottom-color: #e0a800;
}

.card-warning .card-title {
    color: #212529;
}

.card-danger {
    border-color: #dc3545;
}

.card-danger .card-header {
    background: #dc3545;
    color: white;
    border-bottom-color: #bd2130;
}

.card-danger .card-title {
    color: white;
}

.card-info {
    border-color: #17a2b8;
}

.card-info .card-header {
    background: #17a2b8;
    color: white;
    border-bottom-color: #117a8b;
}

.card-info .card-title {
    color: white;
}

@media (max-width: 768px) {

    .card-header,
    .card-body,
    .card-footer {
        padding: 1rem;
    }

    .card-title {
        font-size: 1.1rem;
    }
}
</style>
