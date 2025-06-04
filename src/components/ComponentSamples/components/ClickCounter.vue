<template>
    <div class="click-counter">
        <div class="counter-info">
            <h5>點擊計數器</h5>
            <div class="count-display">
                本地計數: {{ localCount }}
            </div>
        </div>
        <div class="counter-buttons">
            <button @click="handleClick" class="btn btn-primary">
                點擊我 (發送事件)
            </button>
            <button @click="reset" class="btn btn-secondary">
                重置計數
            </button>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['button-clicked'])

const localCount = ref(0)

const handleClick = () => {
    localCount.value++
    emit('button-clicked')  // 發送事件到父組件
}

const reset = () => {
    localCount.value = 0
}
</script>
