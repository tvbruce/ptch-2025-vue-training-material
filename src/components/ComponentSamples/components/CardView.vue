<template>
    <div class="card-view">
        <h5>卡片視圖</h5>
        <div class="cards-container">
            <div v-for="item in items" :key="item.id" class="view-card">
                <div class="card-header">
                    <h6>{{ item.name }}</h6>
                    <span class="card-id">#{{ item.id }}</span>
                </div>
                <div class="card-body">
                    <div v-if="showDetails" class="card-description">
                        {{ item.description }}
                    </div>
                    <div v-else class="card-summary">
                        {{ item.name }} 的基本資訊
                    </div>
                </div>
                <div class="card-footer">
                    <span class="card-type">項目類型</span>
                    <span class="card-status">活躍</span>
                </div>
            </div>
        </div>
        <div class="view-info">
            <p>卡片視圖 - 共 {{ items.length }} 張卡片</p>
            <p>顯示模式: {{ showDetails ? '詳細' : '簡要' }}</p>
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
