<template>
    <div class="emit-demo">
        <h2>Emit 事件處理</h2>
        <p class="route-info">📍 路徑：/ComponentSamples/EmitDemo.vue</p>

        <!-- 基本事件發送 -->
        <div class="demo-section">
            <h3>1. 基本事件發送與接收</h3>
            <div class="result">
                <ClickCounter @button-clicked="handleButtonClick" />
                <div class="event-log">
                    <h5>事件記錄：</h5>
                    <ul>
                        <li v-for="(log, index) in eventLogs" :key="index">
                            {{ log }}
                        </li>
                        <li v-if="eventLogs.length === 0" class="no-events">
                            尚無事件記錄
                        </li>
                    </ul>
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code>// 子組件 ClickCounter.vue
const emit = defineEmits(['button-clicked'])

const handleClick = () => {
  emit('button-clicked')  // 發送事件
}

// 父組件
&lt;ClickCounter @button-clicked="handleButtonClick" /&gt;

const handleButtonClick = () => {
  console.log('接收到按鈕點擊事件')
}</code></pre>
            </div>
        </div>

        <!-- 帶參數的事件 -->
        <div class="demo-section">
            <h3>2. 帶參數的事件傳遞</h3>
            <div class="result">
                <MessageSender @message-sent="handleMessageSent" />
                <div class="message-display">
                    <h5>接收到的訊息：</h5>
                    <div v-for="(msg, index) in messages" :key="index" class="message-item">
                        <strong>{{ msg.sender }}:</strong> {{ msg.content }}
                        <small>({{ msg.timestamp }})</small>
                    </div>
                    <p v-if="messages.length === 0" class="no-messages">
                        尚無訊息
                    </p>
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code>// 子組件 MessageSender.vue
const emit = defineEmits(['message-sent'])

const sendMessage = () => {
  const messageData = {
    content: message.value,
    sender: userName.value,
    timestamp: new Date().toLocaleTimeString()
  }
  emit('message-sent', messageData)  // 傳遞複雜數據
}

// 父組件
const handleMessageSent = (messageData) => {
  messages.value.push(messageData)
}</code></pre>
            </div>
        </div>

        <!-- 事件驗證 -->
        <div class="demo-section">
            <h3>3. 事件參數驗證</h3>
            <div class="result">
                <FormValidator @form-submitted="handleFormSubmit" />
                <div class="validation-results">
                    <h5>表單提交結果：</h5>
                    <div v-if="formResult" class="form-result">
                        <p><strong>狀態:</strong> {{ formResult.status }}</p>
                        <p><strong>訊息:</strong> {{ formResult.message }}</p>
                        <div v-if="formResult.data">
                            <strong>提交的數據:</strong>
                            <pre>{{ JSON.stringify(formResult.data, null, 2) }}</pre>
                        </div>
                    </div>
                    <p v-else class="no-result">尚未提交表單</p>
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code>// 子組件 FormValidator.vue - 帶驗證的事件
const emit = defineEmits({
  'form-submitted': (payload) => {
    // 驗證事件參數
    if (!payload || typeof payload !== 'object') return false
    if (!payload.data || !payload.status) return false
    return ['success', 'error'].includes(payload.status)
  }
})

const submitForm = () => {
  const result = validateForm()
  emit('form-submitted', {
    status: result.isValid ? 'success' : 'error',
    message: result.message,
    data: result.isValid ? formData : null
  })
}</code></pre>
            </div>
        </div>

        <!-- 多個事件處理 -->
        <div class="demo-section">
            <h3>4. 多個事件類型處理</h3>
            <div class="result">
                <FileUploader @upload-start="handleUploadStart" @upload-progress="handleUploadProgress"
                    @upload-complete="handleUploadComplete" @upload-error="handleUploadError" />
                <div class="upload-status">
                    <h5>上傳狀態：</h5>
                    <div class="status-info">
                        <p><strong>狀態:</strong> {{ uploadStatus.status }}</p>
                        <p><strong>進度:</strong> {{ uploadStatus.progress }}%</p>
                        <p v-if="uploadStatus.message"><strong>訊息:</strong> {{ uploadStatus.message }}</p>
                    </div>
                    <div class="progress-bar" v-if="uploadStatus.status === 'uploading'">
                        <div class="progress-fill" :style="{ width: uploadStatus.progress + '%' }"></div>
                    </div>
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code>// 子組件 FileUploader.vue - 多事件類型
const emit = defineEmits([
  'upload-start',
  'upload-progress',
  'upload-complete',
  'upload-error'
])

const startUpload = () => {
  emit('upload-start', { fileName: file.name })

  // 模擬上傳過程
  const interval = setInterval(() => {
    progress.value += 10
    emit('upload-progress', { progress: progress.value })

    if (progress.value >= 100) {
      clearInterval(interval)
      emit('upload-complete', {
        fileName: file.name,
        fileSize: file.size
      })
    }
  }, 200)
}</code></pre>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import ClickCounter from './components/ClickCounter.vue'
import MessageSender from './components/MessageSender.vue'
import FormValidator from './components/FormValidator.vue'
import FileUploader from './components/FileUploader.vue'

// 基本事件處理
const eventLogs = ref([])

// 訊息處理
const messages = ref([])

// 表單驗證結果
const formResult = ref(null)

// 文件上傳狀態
const uploadStatus = ref({
    status: 'idle',
    progress: 0,
    message: ''
})

// 事件處理方法
const handleButtonClick = () => {
    const timestamp = new Date().toLocaleTimeString()
    eventLogs.value.push(`按鈕被點擊 - ${timestamp}`)
}

const handleMessageSent = (messageData) => {
    messages.value.push(messageData)
}

const handleFormSubmit = (result) => {
    formResult.value = result
}

const handleUploadStart = (data) => {
    uploadStatus.value = {
        status: 'uploading',
        progress: 0,
        message: `開始上傳: ${data.fileName}`
    }
}

const handleUploadProgress = (data) => {
    uploadStatus.value.progress = data.progress
}

const handleUploadComplete = (data) => {
    uploadStatus.value = {
        status: 'completed',
        progress: 100,
        message: `上傳完成: ${data.fileName} (${data.fileSize} bytes)`
    }
}

const handleUploadError = (error) => {
    uploadStatus.value = {
        status: 'error',
        progress: 0,
        message: `上傳失敗: ${error.message}`
    }
}
</script>
