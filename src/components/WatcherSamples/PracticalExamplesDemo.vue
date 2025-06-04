<!-- components/WatcherSamples/PracticalExamplesDemo.vue -->
<template>
    <div class="practical-examples-demo">
        <h2>實際應用範例</h2>
        <p class="route-info">📍 路徑：/WatcherSamples/PracticalExamplesDemo.vue</p>

        <!-- 搜索防抖 -->
        <div class="demo-section">
            <h3>1. 搜索防抖（Debounce）</h3>
            <div class="description">
                使用 watch 來實現搜索防抖，避免頻繁的 API 呼叫。
            </div>
            <div class="controls">
                <input v-model="searchTerm" placeholder="輸入搜索關鍵字" class="input-field">
                <input v-model.number="debounceDelay" type="number" min="100" max="2000" class="input-field"
                    placeholder="防抖延遲 (ms)">
            </div>
            <div class="result">
                <div class="display-value">
                    <strong>搜索關鍵字：</strong>{{ searchTerm }}
                </div>
                <div class="display-value">
                    <strong>實際搜索：</strong>{{ actualSearchTerm }}
                </div>
                <div class="display-value">
                    <strong>結果數量：</strong>{{ searchResults.length }} 筆
                </div>
                <div class="display-value">
                    <strong>API 呼叫：</strong>{{ searchApiCalls }} 次
                </div>
                <div class="display-value">
                    <strong>輸入次數：</strong>{{ inputCount }} 次
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code>import { ref, watch } from 'vue'

const searchTerm = ref('')
const actualSearchTerm = ref('')
let searchTimeout = null

// 使用 watch 實現防抖
watch(searchTerm, (newValue) => {
  // 清除之前的計時器
  if (searchTimeout) {
    clearTimeout(searchTimeout)
  }

  // 設置新的計時器
  searchTimeout = setTimeout(async () => {
    actualSearchTerm.value = newValue
    if (newValue.trim()) {
      await performSearch(newValue)
    }
  }, debounceDelay.value)
})</code></pre>
            </div>
        </div>

        <!-- 表單驗證 -->
        <div class="demo-section">
            <h3>2. 即時表單驗證</h3>
            <div class="description">
                使用 watchEffect 來實現複雜的表單驗證邏輯。
            </div>
            <div class="controls">
                <input v-model="formData.username" placeholder="用戶名" class="input-field">
                <input v-model="formData.email" placeholder="電子郵件" class="input-field">
                <input v-model="formData.password" type="password" placeholder="密碼" class="input-field">
                <input v-model="formData.confirmPassword" type="password" placeholder="確認密碼" class="input-field">
            </div>
            <div class="result">
                <div class="validation-results">
                    <div v-for="(error, field) in validationErrors" :key="field" class="display-value"
                        :class="error ? 'warning' : 'success'">
                        <strong>{{ getFieldLabel(field) }}：</strong>
                        {{ error || '✓ 驗證通過' }}
                    </div>
                    <div class="display-value" :class="isFormValid ? 'success' : 'warning'">
                        <strong>整體表單：</strong>{{ isFormValid ? '✓ 可以提交' : '❌ 還有錯誤' }}
                    </div>
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code>// 使用 watchEffect 監控整個表單
watchEffect(() => {
  const errors = {}

  // 驗證邏輯
  if (!formData.value.username) {
    errors.username = '請輸入用戶名'
  } else if (formData.value.username.length &lt; 3) {
    errors.username = '用戶名至少 3 個字符'
  }

  // 其他驗證...
  validationErrors.value = errors
})</code></pre>
            </div>
        </div>

        <!-- 本地存儲同步 -->
        <div class="demo-section">
            <h3>3. 本地存儲同步</h3>
            <div class="description">
                使用 watch 自動將數據同步到本地存儲。
            </div>
            <div class="controls">
                <div class="setting-group">
                    <label>主題設定：</label>
                    <select v-model="userSettings.theme" class="select-field">
                        <option value="light">淺色</option>
                        <option value="dark">深色</option>
                        <option value="auto">自動</option>
                    </select>
                </div>
                <div class="setting-group">
                    <label>語言設定：</label>
                    <select v-model="userSettings.language" class="select-field">
                        <option value="zh-TW">繁體中文</option>
                        <option value="zh-CN">簡體中文</option>
                        <option value="en">English</option>
                    </select>
                </div>
                <div class="setting-group">
                    <label class="checkbox-label">
                        <input type="checkbox" v-model="userSettings.notifications">
                        接收通知
                    </label>
                </div>
                <button @click="clearStorage" class="btn btn-warning">清除本地存儲</button>
            </div>
            <div class="result">
                <div class="display-value">
                    <strong>當前設定：</strong>
                    <pre class="object-display">{{ JSON.stringify(userSettings, null, 2) }}</pre>
                </div>
                <div class="display-value">
                    <strong>儲存次數：</strong>{{ saveCount }}
                </div>
                <div class="display-value">
                    <strong>載入次數：</strong>{{ loadCount }}
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code>// 監聽設定變化並保存到本地存儲
watch(userSettings, (newSettings) => {
  localStorage.setItem('userSettings', JSON.stringify(newSettings))
  saveCount.value++
}, { deep: true })

// 組件初始化時載入設定
onMounted(() => {
  const saved = localStorage.getItem('userSettings')
  if (saved) {
    userSettings.value = JSON.parse(saved)
    loadCount.value++
  }
})</code></pre>
            </div>
        </div>

        <!-- 數據轉換鏈 -->
        <div class="demo-section">
            <h3>4. 數據轉換鏈</h3>
            <div class="description">
                使用 watchEffect 建立數據轉換的依賴鏈。
            </div>
            <div class="controls">
                <input v-model="rawInput" placeholder="輸入原始數據" class="input-field">
                <label class="checkbox-label">
                    <input type="checkbox" v-model="enableUppercase">
                    轉換為大寫
                </label>
                <label class="checkbox-label">
                    <input type="checkbox" v-model="enableReverse">
                    反向排列
                </label>
                <label class="checkbox-label">
                    <input type="checkbox" v-model="enableSort">
                    字母排序
                </label>
            </div>
            <div class="result">
                <div class="transformation-chain">
                    <div class="transform-step">
                        <strong>原始數據：</strong>{{ rawInput }}
                    </div>
                    <div class="transform-step">
                        <strong>步驟 1（大寫）：</strong>{{ step1Result }}
                    </div>
                    <div class="transform-step">
                        <strong>步驟 2（反向）：</strong>{{ step2Result }}
                    </div>
                    <div class="transform-step">
                        <strong>步驟 3（排序）：</strong>{{ step3Result }}
                    </div>
                    <div class="transform-step final">
                        <strong>最終結果：</strong>{{ finalResult }}
                    </div>
                </div>
                <div class="display-value">
                    <strong>轉換次數：</strong>{{ transformCount }}
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code>// 建立轉換鏈
watchEffect(() => {
  step1Result.value = enableUppercase.value
    ? rawInput.value.toUpperCase()
    : rawInput.value
})

watchEffect(() => {
  step2Result.value = enableReverse.value
    ? step1Result.value.split('').reverse().join('')
    : step1Result.value
})

// 其他轉換步驟...</code></pre>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, watch, watchEffect, onMounted } from 'vue'

// 搜索防抖
const searchTerm = ref('')
const actualSearchTerm = ref('')
const searchResults = ref([])
const searchApiCalls = ref(0)
const inputCount = ref(0)
const debounceDelay = ref(500)
let searchTimeout = null

const performSearch = async (term) => {
    searchApiCalls.value++
    await new Promise(resolve => setTimeout(resolve, 200))
    searchResults.value = Array.from({ length: Math.floor(Math.random() * 10) + 1 }, (_, i) => ({
        id: i,
        title: `${term} 相關結果 ${i + 1}`
    }))
}

watch(searchTerm, (newValue) => {
    inputCount.value++

    if (searchTimeout) {
        clearTimeout(searchTimeout)
    }

    searchTimeout = setTimeout(async () => {
        actualSearchTerm.value = newValue
        if (newValue.trim()) {
            await performSearch(newValue)
        } else {
            searchResults.value = []
        }
    }, debounceDelay.value)
})

// 表單驗證
const formData = ref({
    username: '',
    email: '',
    password: '',
    confirmPassword: ''
})
const validationErrors = ref({})
const isFormValid = ref(false)

const isValidEmail = (email) => {
    return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)
}

const getFieldLabel = (field) => {
    const labels = {
        username: '用戶名',
        email: '電子郵件',
        password: '密碼',
        confirmPassword: '確認密碼'
    }
    return labels[field] || field
}

watchEffect(() => {
    const errors = {}

    if (!formData.value.username) {
        errors.username = '請輸入用戶名'
    } else if (formData.value.username.length < 3) {
        errors.username = '用戶名至少 3 個字符'
    }

    if (!formData.value.email) {
        errors.email = '請輸入郵件'
    } else if (!isValidEmail(formData.value.email)) {
        errors.email = '郵件格式不正確'
    }

    if (!formData.value.password) {
        errors.password = '請輸入密碼'
    } else if (formData.value.password.length < 6) {
        errors.password = '密碼至少 6 個字符'
    }

    if (formData.value.confirmPassword && formData.value.password !== formData.value.confirmPassword) {
        errors.confirmPassword = '密碼不一致'
    }

    validationErrors.value = errors
    isFormValid.value = Object.keys(errors).length === 0 &&
        formData.value.username &&
        formData.value.email &&
        formData.value.password &&
        formData.value.confirmPassword
})

// 本地存儲同步
const userSettings = ref({
    theme: 'light',
    language: 'zh-TW',
    notifications: true
})
const saveCount = ref(0)
const loadCount = ref(0)

watch(userSettings, (newSettings) => {
    localStorage.setItem('userSettings', JSON.stringify(newSettings))
    saveCount.value++
}, { deep: true })

onMounted(() => {
    const saved = localStorage.getItem('userSettings')
    if (saved) {
        try {
            userSettings.value = JSON.parse(saved)
            loadCount.value++
        } catch {
            console.warn('無法載入本地設定')
        }
    }
})

const clearStorage = () => {
    localStorage.removeItem('userSettings')
    userSettings.value = {
        theme: 'light',
        language: 'zh-TW',
        notifications: true
    }
    saveCount.value = 0
    loadCount.value = 0
}

// 數據轉換鏈
const rawInput = ref('')
const enableUppercase = ref(false)
const enableReverse = ref(false)
const enableSort = ref(false)
const step1Result = ref('')
const step2Result = ref('')
const step3Result = ref('')
const finalResult = ref('')
const transformCount = ref(0)

watchEffect(() => {
    step1Result.value = enableUppercase.value
        ? rawInput.value.toUpperCase()
        : rawInput.value
})

watchEffect(() => {
    step2Result.value = enableReverse.value
        ? step1Result.value.split('').reverse().join('')
        : step1Result.value
})

watchEffect(() => {
    step3Result.value = enableSort.value
        ? step2Result.value.split('').sort().join('')
        : step2Result.value
})

watchEffect(() => {
    finalResult.value = step3Result.value
    transformCount.value++
})
</script>
