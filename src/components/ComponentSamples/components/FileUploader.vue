<template>
    <div class="file-uploader">
        <div class="upload-section">
            <h5>文件上傳模擬器</h5>
            <div class="file-input-area">
                <input type="file" @change="handleFileSelect" class="file-input" :disabled="isUploading">
                <div v-if="selectedFile" class="file-info">
                    <p><strong>檔案:</strong> {{ selectedFile.name }}</p>
                    <p><strong>大小:</strong> {{ formatFileSize(selectedFile.size) }}</p>
                    <p><strong>類型:</strong> {{ selectedFile.type || '未知' }}</p>
                </div>
            </div>

            <div class="upload-controls">
                <button @click="startUpload" :disabled="!selectedFile || isUploading" class="btn btn-primary">
                    {{ isUploading ? '上傳中...' : '開始上傳' }}
                </button>
                <button @click="cancelUpload" :disabled="!isUploading" class="btn btn-warning">
                    取消上傳
                </button>
                <button @click="reset" class="btn btn-secondary">
                    重置
                </button>
            </div>

            <div class="upload-options">
                <label class="checkbox-label">
                    <input type="checkbox" v-model="simulateError">
                    模擬上傳錯誤
                </label>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits([
    'upload-start',
    'upload-progress',
    'upload-complete',
    'upload-error'
])

const selectedFile = ref(null)
const isUploading = ref(false)
const simulateError = ref(false)
let uploadInterval = null

const handleFileSelect = (event) => {
    const file = event.target.files[0]
    if (file) {
        selectedFile.value = file
    }
}

const formatFileSize = (bytes) => {
    if (bytes === 0) return '0 Bytes'
    const k = 1024
    const sizes = ['Bytes', 'KB', 'MB', 'GB']
    const i = Math.floor(Math.log(bytes) / Math.log(k))
    return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i]
}

const startUpload = () => {
    if (!selectedFile.value || isUploading.value) return

    isUploading.value = true
    let progress = 0

    // 發送開始上傳事件
    emit('upload-start', {
        fileName: selectedFile.value.name,
        fileSize: selectedFile.value.size
    })

    // 模擬上傳過程
    uploadInterval = setInterval(() => {
        progress += Math.random() * 15 + 5  // 隨機進度增長

        if (progress >= 100) {
            progress = 100
            clearInterval(uploadInterval)
            uploadInterval = null
            isUploading.value = false

            if (simulateError.value) {
                // 模擬錯誤
                emit('upload-error', {
                    message: '網路連線錯誤',
                    code: 'NETWORK_ERROR'
                })
            } else {
                // 上傳完成
                emit('upload-complete', {
                    fileName: selectedFile.value.name,
                    fileSize: selectedFile.value.size,
                    uploadTime: new Date().toLocaleTimeString()
                })
            }
        } else {
            // 發送進度更新
            emit('upload-progress', { progress: Math.round(progress) })
        }
    }, 200)
}

const cancelUpload = () => {
    if (uploadInterval) {
        clearInterval(uploadInterval)
        uploadInterval = null
    }
    isUploading.value = false

    emit('upload-error', {
        message: '用戶取消上傳',
        code: 'USER_CANCELLED'
    })
}

const reset = () => {
    if (uploadInterval) {
        clearInterval(uploadInterval)
        uploadInterval = null
    }
    selectedFile.value = null
    isUploading.value = false
    simulateError.value = false
}
</script>
