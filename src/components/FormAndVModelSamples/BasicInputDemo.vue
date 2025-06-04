<!-- components/FormAndVModelSamples/BasicInputDemo.vue -->
<template>
    <div class="basic-input-demo">
        <h2>基礎輸入框 (v-model)</h2>
        <p class="route-info">📍 路徑：/FormAndVModelSamples/BasicInputDemo.vue</p>

        <!-- 文本輸入 -->
        <div class="demo-section">
            <h3>1. 文本輸入框</h3>
            <div class="demo-grid">
                <div class="demo-item">
                    <label>單行文本：</label>
                    <input type="text" v-model="textValue" placeholder="請輸入文本">
                    <div class="output">輸入值：{{ textValue }}</div>
                </div>

                <div class="demo-item">
                    <label>多行文本：</label>
                    <textarea v-model="textareaValue" placeholder="請輸入多行文本" rows="3"></textarea>
                    <div class="output">輸入值：{{ textareaValue }}</div>
                </div>
            </div>

            <div class="code-example">
                <pre v-pre><code>&lt;!-- 單行文本 --&gt;
&lt;input type="text" v-model="textValue" placeholder="請輸入文本"&gt;

&lt;!-- 多行文本 --&gt;
&lt;textarea v-model="textareaValue" placeholder="請輸入多行文本"&gt;&lt;/textarea&gt;

// 響應式數據
const textValue = ref('')
const textareaValue = ref('')</code></pre>
            </div>
        </div>

        <!-- 密碼輸入 -->
        <div class="demo-section">
            <h3>2. 密碼輸入框</h3>
            <div class="demo-grid">
                <div class="demo-item">
                    <label>密碼：</label>
                    <div class="password-reveal">
                        <input :type="showPassword ? 'text' : 'password'" v-model="passwordValue" placeholder="請輸入密碼">
                        <button type="button" @click="showPassword = !showPassword" class="toggle-btn">
                            {{ showPassword ? '隱藏' : '顯示' }}
                        </button>
                    </div>
                    <div class="output">輸入長度：{{ passwordValue.length }} 字元</div>
                    <div class="validation"
                        :class="{ valid: passwordValue.length >= 6, invalid: passwordValue.length > 0 && passwordValue.length < 6 }">
                        {{ passwordValue.length >= 6 ? '✅ 密碼強度足夠' : '❌ 密碼至少需要6個字元' }}
                    </div>
                </div>
            </div>

            <div class="code-example">
                <pre v-pre><code>&lt;!-- 密碼輸入框 --&gt;
&lt;input
  :type="showPassword ? 'text' : 'password'"
  v-model="passwordValue"
  placeholder="請輸入密碼"
&gt;

// 響應式數據
const passwordValue = ref('')
const showPassword = ref(false)</code></pre>
            </div>
        </div>

        <!-- 數字輸入 -->
        <div class="demo-section">
            <h3>3. 數字輸入框</h3>
            <div class="demo-grid">
                <div class="demo-item">
                    <label>數量 (1-100)：</label>
                    <input type="number" v-model.number="numberValue" min="1" max="100" placeholder="輸入數字">
                    <div class="output">
                        <div>輸入值：{{ numberValue }}</div>
                        <div>資料型別：{{ typeof numberValue }}</div>
                        <div>有效範圍：{{ numberValue >= 1 && numberValue <= 100 ? '是' : '否' }}</div>
                        </div>
                    </div>

                    <div class="demo-item">
                        <label>價格：</label>
                        <input type="number" v-model.number="priceValue" step="0.01" min="0" placeholder="輸入價格">
                        <div class="output">
                            <div>價格：NT$ {{ priceValue ? priceValue.toFixed(2) : '0.00' }}</div>
                            <div>含稅價格：NT$ {{ priceValue ? (priceValue * 1.05).toFixed(2) : '0.00' }}</div>
                        </div>
                    </div>
                </div>

                <div class="code-example">
                    <pre v-pre><code>&lt;!-- 數字輸入框 --&gt;
&lt;input type="number" v-model.number="numberValue" min="1" max="100"&gt;
&lt;input type="number" v-model.number="priceValue" step="0.01" min="0"&gt;

// 響應式數據
const numberValue = ref(null)
const priceValue = ref(null)</code></pre>
                </div>
            </div>

            <!-- 日期時間輸入 -->
            <div class="demo-section">
                <h3>4. 日期時間輸入</h3>
                <div class="demo-grid">
                    <div class="demo-item">
                        <label>日期：</label>
                        <input type="date" v-model="dateValue">
                        <div class="output">
                            <div>選擇日期：{{ dateValue }}</div>
                            <div class="formatted-date" v-if="dateValue">
                                格式化顯示：{{ formatDate(dateValue) }}
                            </div>
                        </div>
                    </div>

                    <div class="demo-item">
                        <label>時間：</label>
                        <input type="time" v-model="timeValue">
                        <div class="output">
                            <div>選擇時間：{{ timeValue }}</div>
                            <div v-if="timeValue">
                                12小時制：{{ formatTime(timeValue) }}
                            </div>
                        </div>
                    </div>

                    <div class="demo-item">
                        <label>日期時間：</label>
                        <input type="datetime-local" v-model="datetimeValue">
                        <div class="output">
                            <div>完整時間：{{ datetimeValue }}</div>
                            <div class="formatted-date" v-if="datetimeValue">
                                格式化：{{ formatDateTime(datetimeValue) }}
                            </div>
                        </div>
                    </div>
                </div>

                <div class="code-example">
                    <pre v-pre><code>&lt;!-- 日期時間輸入 --&gt;
&lt;input type="date" v-model="dateValue"&gt;
&lt;input type="time" v-model="timeValue"&gt;
&lt;input type="datetime-local" v-model="datetimeValue"&gt;

// 響應式數據
const dateValue = ref('')
const timeValue = ref('')
const datetimeValue = ref('')</code></pre>
                </div>
            </div>

            <!-- 檔案輸入 -->
            <div class="demo-section">
                <h3>5. 檔案輸入</h3>
                <div class="demo-grid">
                    <div class="demo-item">
                        <label>單個檔案：</label>
                        <input type="file" @change="handleFileChange" accept="image/*">
                        <div class="output" v-if="selectedFile">
                            <div>檔案名稱：{{ selectedFile.name }}</div>
                            <div>檔案大小：{{ formatFileSize(selectedFile.size) }}</div>
                            <div>檔案類型：{{ selectedFile.type }}</div>
                        </div>
                    </div>

                    <div class="demo-item">
                        <label>多個檔案：</label>
                        <input type="file" @change="handleMultipleFileChange" multiple>
                        <div class="output" v-if="selectedFiles.length > 0">
                            <div>選擇了 {{ selectedFiles.length }} 個檔案</div>
                            <ul>
                                <li v-for="file in selectedFiles" :key="file.name">
                                    {{ file.name }} ({{ formatFileSize(file.size) }})
                                </li>
                            </ul>
                        </div>
                    </div>
                </div>

                <div class="info-box">
                    <h4>📝 注意事項</h4>
                    <p>檔案輸入框不能直接使用 v-model，需要監聽 change 事件來獲取檔案資訊。</p>
                </div>

                <div class="code-example">
                    <pre v-pre><code>&lt;!-- 檔案輸入 --&gt;
&lt;input type="file" @change="handleFileChange" accept="image/*"&gt;
&lt;input type="file" @change="handleMultipleFileChange" multiple&gt;

// 處理檔案變更
const handleFileChange = (event) => {
  selectedFile.value = event.target.files[0] || null
}

const handleMultipleFileChange = (event) => {
  selectedFiles.value = Array.from(event.target.files)
}</code></pre>
                </div>
            </div>
        </div>
</template>

<script setup>
import { ref } from 'vue'

// 文本輸入
const textValue = ref('')
const textareaValue = ref('')

// 密碼輸入
const passwordValue = ref('')
const showPassword = ref(false)

// 數字輸入
const numberValue = ref(null)
const priceValue = ref(null)

// 日期時間輸入
const dateValue = ref('')
const timeValue = ref('')
const datetimeValue = ref('')

// 檔案輸入
const selectedFile = ref(null)
const selectedFiles = ref([])

// 處理檔案變更
const handleFileChange = (event) => {
    selectedFile.value = event.target.files[0] || null
}

const handleMultipleFileChange = (event) => {
    selectedFiles.value = Array.from(event.target.files)
}

// 工具函數
const formatDate = (dateStr) => {
    if (!dateStr) return ''
    const date = new Date(dateStr)
    return date.toLocaleDateString('zh-TW', {
        year: 'numeric',
        month: 'long',
        day: 'numeric',
        weekday: 'long'
    })
}

const formatTime = (timeStr) => {
    if (!timeStr) return ''
    const [hours, minutes] = timeStr.split(':')
    const hour12 = hours % 12 || 12
    const ampm = hours >= 12 ? '下午' : '上午'
    return `${ampm} ${hour12}:${minutes}`
}

const formatDateTime = (datetimeStr) => {
    if (!datetimeStr) return ''
    const date = new Date(datetimeStr)
    return date.toLocaleString('zh-TW', {
        year: 'numeric',
        month: 'long',
        day: 'numeric',
        weekday: 'long',
        hour: '2-digit',
        minute: '2-digit'
    })
}

const formatFileSize = (bytes) => {
    if (bytes === 0) return '0 Bytes'
    const k = 1024
    const sizes = ['Bytes', 'KB', 'MB', 'GB']
    const i = Math.floor(Math.log(bytes) / Math.log(k))
    return parseFloat((bytes / Math.pow(k, i)).toFixed(2)) + ' ' + sizes[i]
}
</script>
