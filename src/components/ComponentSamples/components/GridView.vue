<template>
    <div class="grid-view">
        <h5>網格視圖</h5>
        <div class="grid-container">
            <div v-for="item in items" :key="item.id" class="grid-item">
                <div class="item-header">
                    <span class="item-id">{{ item.id }}</span>
                    <span class="item-badge">項目</span>
                </div>
                <div class="item-title">{{ item.name }}</div>
                <div v-if="showDetails" class="item-description">
                    {{ item.description }}
                </div>
            </div>
        </div>
        <div class="view-info">
            <p>網格模式 - {{ items.length }} 項目</p>
            <p>詳細模式: {{ showDetails ? '開啟' : '關閉' }}</p>
        </div>
    </div>
</template>

<script setup>
defineProps({
    items: {
        type: Array,
        default: () => []
    },
    showDetails: {
        type: Boolean,
        default: false
    }
})
</script>
