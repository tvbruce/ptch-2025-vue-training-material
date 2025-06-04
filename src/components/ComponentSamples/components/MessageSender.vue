<template>
    <div class="message-sender">
        <div class="form-section">
            <h5>發送訊息</h5>
            <div class="input-group">
                <input v-model="userName" placeholder="您的姓名" class="input-field">
                <textarea v-model="message" placeholder="輸入訊息..." class="textarea-field" rows="3"></textarea>
            </div>
            <div class="form-actions">
                <button @click="sendMessage" :disabled="!canSend" class="btn btn-primary">
                    發送訊息
                </button>
                <button @click="clearForm" class="btn btn-secondary">
                    清除
                </button>
            </div>
        </div>
        <div class="message-info">
            <p>字數: {{ message.length }}/200</p>
            <p v-if="!userName.trim()" class="warning">請輸入姓名</p>
            <p v-if="!message.trim()" class="warning">請輸入訊息內容</p>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const emit = defineEmits(['message-sent'])

const userName = ref('使用者')
const message = ref('')

const canSend = computed(() => {
    return userName.value.trim() && message.value.trim() && message.value.length <= 200
})

const sendMessage = () => {
    if (!canSend.value) return

    const messageData = {
        content: message.value.trim(),
        sender: userName.value.trim(),
        timestamp: new Date().toLocaleTimeString()
    }

    emit('message-sent', messageData)  // 傳遞複雜數據

    // 清除訊息內容但保留姓名
    message.value = ''
}

const clearForm = () => {
    userName.value = ''
    message.value = ''
}
</script>
