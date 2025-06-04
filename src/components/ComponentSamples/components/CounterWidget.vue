<template>
    <div class="counter-widget">
        <h5>計數器小工具</h5>
        <div class="widget-content">
            <div class="count-display">
                計數值: {{ count }}
            </div>
            <div class="widget-controls">
                <button @click="decrement" class="btn btn-secondary">-</button>
                <button @click="increment" class="btn btn-primary">+</button>
                <button @click="reset" class="btn btn-warning">重置</button>
            </div>
            <div class="widget-info">
                <p>總操作次數: {{ operationCount }}</p>
                <p>最後操作: {{ lastAction || '無' }}</p>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['widget-action', 'value-changed'])

const count = ref(0)
const operationCount = ref(0)
const lastAction = ref('')

const increment = () => {
    count.value++
    operationCount.value++
    lastAction.value = '增加'
    emit('widget-action', '增加計數')
    emit('value-changed', count.value)
}

const decrement = () => {
    count.value--
    operationCount.value++
    lastAction.value = '減少'
    emit('widget-action', '減少計數')
    emit('value-changed', count.value)
}

const reset = () => {
    count.value = 0
    operationCount.value++
    lastAction.value = '重置'
    emit('widget-action', '重置計數')
    emit('value-changed', count.value)
}
</script>
