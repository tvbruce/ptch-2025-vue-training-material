<template>
    <div class="home-tab">
        <h4>{{ tabData.message || '歡迎來到首頁!' }}</h4>
        <div class="home-content">
            <p>這是首頁標籤的內容。當前時間：{{ currentTime }}</p>
            <div class="home-stats">
                <div class="stat-item">
                    <span class="stat-value">{{ visitCount }}</span>
                    <span class="stat-label">訪問次數</span>
                </div>
                <div class="stat-item">
                    <span class="stat-value">{{ onlineTime }}s</span>
                    <span class="stat-label">在線時間</span>
                </div>
            </div>
            <button @click="visitCount++" class="btn btn-primary">
                增加訪問次數
            </button>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

defineProps({
    tabData: {
        type: Object,
        default: () => ({})
    }
})

const currentTime = ref(new Date().toLocaleTimeString())
const visitCount = ref(0)
const onlineTime = ref(0)
let timeInterval = null

onMounted(() => {
    timeInterval = setInterval(() => {
        currentTime.value = new Date().toLocaleTimeString()
        onlineTime.value++
    }, 1000)
})

onUnmounted(() => {
    if (timeInterval) {
        clearInterval(timeInterval)
    }
})
</script>
