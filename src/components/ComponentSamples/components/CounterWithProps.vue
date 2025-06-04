<template>
    <div class="counter-with-props">
        <div class="counter-display">
            <h5>計數器值: {{ localValue }}</h5>
            <div class="counter-info">
                <p>初始值: {{ props.initialValue }}</p>
                <p>當前值: {{ localValue }}</p>
                <p>已變更: {{ hasChanged ? '是' : '否' }}</p>
            </div>
        </div>
        <div class="counter-controls">
            <button @click="decrement" class="btn btn-secondary">-1</button>
            <button @click="increment" class="btn btn-primary">+1</button>
            <button @click="reset" class="btn btn-warning">重置</button>
        </div>
        <div class="info-box">
            <p>這個組件展示了正確的 Props 處理方式：</p>
            <ul>
                <li>使用本地狀態接收 props 值</li>
                <li>通過 emit 事件通知父組件值的變更</li>
                <li>不直接修改 props</li>
            </ul>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue'

const props = defineProps({
    initialValue: {
        type: Number,
        default: 0
    }
})

const emit = defineEmits(['update:value'])

// 使用本地狀態接收 props 值
const localValue = ref(props.initialValue)

// 計算是否已變更
const hasChanged = computed(() => {
    return localValue.value !== props.initialValue
})

// 監聽 props 變化，同步更新本地值
watch(() => props.initialValue, (newValue) => {
    localValue.value = newValue
})

// 方法
const increment = () => {
    localValue.value++
    emit('update:value', localValue.value)
}

const decrement = () => {
    localValue.value--
    emit('update:value', localValue.value)
}

const reset = () => {
    localValue.value = props.initialValue
    emit('update:value', localValue.value)
}
</script>
