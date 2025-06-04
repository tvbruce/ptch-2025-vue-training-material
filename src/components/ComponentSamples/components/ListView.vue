<template>
    <div class="list-view">
        <h5>列表視圖</h5>
        <div class="list-container">
            <div v-for="item in items" :key="item.id" class="list-item">
                <div class="item-index">{{ item.id }}</div>
                <div class="item-content">
                    <h6>{{ item.name }}</h6>
                    <p v-if="showDetails">{{ item.description }}</p>
                </div>
                <div class="item-status">
                    <span class="status-badge">項目</span>
                </div>
            </div>
        </div>
        <div class="view-info">
            <p>總計: {{ items.length }} 個項目</p>
            <p>顯示詳細: {{ showDetails ? '是' : '否' }}</p>
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
