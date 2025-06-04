<!-- components/LifecycleSamples/ChildComponent.vue -->
<template>
  <div class="child-component">
    <h4>子組件</h4>
    <div class="child-content">
      <p>這是一個子組件，用來展示生命週期</p>
      <div class="child-data">
        <input v-model="childMessage" placeholder="子組件數據" class="input-field">
        <div class="display-value">
          值：{{ childMessage }}
        </div>
      </div>
      <div class="child-timer">
        <span>存活時間：{{ aliveTime }} 秒</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onUpdated, onUnmounted } from 'vue'

const emit = defineEmits(['lifecycle-event'])

const childMessage = ref('子組件訊息')
const aliveTime = ref(0)
let timer = null

const emitLifecycleEvent = (hook, message, type) => {
  emit('lifecycle-event', { hook, message, type })
}

onMounted(() => {
  emitLifecycleEvent('onMounted', '子組件已掛載', 'success')

  // 啟動計時器
  timer = setInterval(() => {
    aliveTime.value++
  }, 1000)
})

onUpdated(() => {
  emitLifecycleEvent('onUpdated', '子組件已更新', 'warning')
})

onUnmounted(() => {
  emitLifecycleEvent('onUnmounted', '子組件即將卸載', 'error')

  // 清除計時器
  if (timer) {
    clearInterval(timer)
  }
})
</script>

<style scoped>
/* 樣式已在 src/assets/main.css 中定義 */
</style>
