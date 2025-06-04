<template>
    <div class="timer-widget">
        <h5>計時器小工具</h5>
        <div class="widget-content">
            <div class="time-display">
                {{ formatTime(seconds) }}
            </div>
            <div class="widget-controls">
                <button @click="start" :disabled="isRunning" class="btn btn-success">開始</button>
                <button @click="pause" :disabled="!isRunning" class="btn btn-warning">暫停</button>
                <button @click="reset" class="btn btn-secondary">重置</button>
            </div>
            <div class="widget-info">
                <p>狀態: {{ isRunning ? '運行中' : '已停止' }}</p>
                <p>總運行次數: {{ runCount }}</p>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, onUnmounted } from 'vue'

const emit = defineEmits(['widget-action', 'value-changed'])

const seconds = ref(0)
const isRunning = ref(false)
const runCount = ref(0)
let timer = null

const formatTime = (totalSeconds) => {
    const minutes = Math.floor(totalSeconds / 60)
    const secs = totalSeconds % 60
    return `${minutes.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`
}

const start = () => {
    if (!isRunning.value) {
        isRunning.value = true
        runCount.value++
        timer = setInterval(() => {
            seconds.value++
            emit('value-changed', seconds.value)
        }, 1000)
        emit('widget-action', '開始計時')
    }
}

const pause = () => {
    if (isRunning.value) {
        isRunning.value = false
        if (timer) {
            clearInterval(timer)
            timer = null
        }
        emit('widget-action', '暫停計時')
    }
}

const reset = () => {
    isRunning.value = false
    if (timer) {
        clearInterval(timer)
        timer = null
    }
    seconds.value = 0
    emit('widget-action', '重置計時')
    emit('value-changed', seconds.value)
}

onUnmounted(() => {
    if (timer) {
        clearInterval(timer)
    }
})
</script>
