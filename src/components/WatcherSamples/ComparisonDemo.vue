<!-- components/WatcherSamples/ComparisonDemo.vue -->
<template>
    <div class="comparison-demo">
        <h2>watch 與 watchEffect 對比</h2>
        <p class="route-info">📍 路徑：/WatcherSamples/ComparisonDemo.vue</p>

        <!-- 選擇建議 -->
        <div class="demo-section">
            <h3>何時使用哪一個？</h3>
            <div class="comparison-grid">
                <div class="comparison-card watch-card">
                    <h4>🎯 使用 watch 當你需要：</h4>
                    <ul>
                        <li>明確指定要偵聽的數據源</li>
                        <li>獲取變化前後的值（oldValue, newValue）</li>
                        <li>根據特定數據變化執行副作用</li>
                        <li>更精確的控制何時觸發</li>
                        <li>偵聽多個獨立的數據源</li>
                    </ul>
                </div>
                <div class="comparison-card watcheffect-card">
                    <h4>⚡ 使用 watchEffect 當你需要：</h4>
                    <ul>
                        <li>自動追蹤所有依賴的響應式數據</li>
                        <li>立即執行一次（初始化）</li>
                        <li>不需要知道變化前的值</li>
                        <li>更簡潔的語法</li>
                        <li>類似 React useEffect 的行為</li>
                    </ul>
                </div>
            </div>
        </div>

        <!-- 實際案例對比 -->
        <div class="demo-section">
            <h3>實際案例對比</h3>

            <!-- 用戶資料驗證 -->
            <div class="case-example">
                <h4>案例 1：用戶資料驗證</h4>
                <div class="controls">
                    <input v-model="userEmail" placeholder="輸入電子郵件" class="input-field">
                    <input v-model="userPassword" type="password" placeholder="輸入密碼" class="input-field">
                </div>

                <div class="demo-container">
                    <div class="demo-panel">
                        <h5>使用 watch 的方式</h5>
                        <div class="result">
                            <div class="display-value" :class="emailValidation.class">
                                <strong>Email 驗證：</strong>{{ emailValidation.message }}
                            </div>
                            <div class="display-value" :class="passwordValidation.class">
                                <strong>密碼驗證：</strong>{{ passwordValidation.message }}
                            </div>
                            <div class="display-value">
                                <strong>watch 觸發次數：</strong>{{ watchValidationCount }}
                            </div>
                        </div>
                        <div class="code-example">
                            <pre v-pre><code>// 使用 watch：精確控制每個欄位
watch(userEmail, (newEmail) => {
  if (!newEmail) {
    emailValidation.value = { message: '請輸入郵件', class: 'warning' }
  } else if (isValidEmail(newEmail)) {
    emailValidation.value = { message: '郵件格式正確', class: 'success' }
  } else {
    emailValidation.value = { message: '郵件格式錯誤', class: 'warning' }
  }
})

watch(userPassword, (newPassword) => {
  // 精確控制密碼驗證邏輯
})</code></pre>
                        </div>
                    </div>

                    <div class="demo-panel">
                        <h5>使用 watchEffect 的方式</h5>
                        <div class="result">
                            <div class="display-value" :class="effectFormValidation.isValid ? 'success' : 'warning'">
                                <strong>整體表單狀態：</strong>{{ effectFormValidation.message }}
                            </div>
                            <div class="display-value">
                                <strong>watchEffect 執行次數：</strong>{{ watchEffectValidationCount }}
                            </div>
                        </div>
                        <div class="code-example">
                            <pre v-pre><code>// 使用 watchEffect：自動追蹤所有相關狀態
watchEffect(() => {
  const emailValid = isValidEmail(userEmail.value)
  const passwordValid = userPassword.value.length >= 6

  effectFormValidation.value = {
    isValid: emailValid && passwordValid,
    message: emailValid && passwordValid
      ? '表單填寫完整'
      : '請完整填寫表單'
  }
})</code></pre>
                        </div>
                    </div>
                </div>
            </div>

            <!-- API 數據獲取 -->
            <div class="case-example">
                <h4>案例 2：API 數據獲取</h4>
                <div class="controls">
                    <select v-model="selectedUserId" class="select-field">
                        <option value="">選擇用戶</option>
                        <option value="1">用戶 1</option>
                        <option value="2">用戶 2</option>
                        <option value="3">用戶 3</option>
                    </select>
                    <input v-model="searchQuery" placeholder="搜索關鍵字" class="input-field">
                </div>

                <div class="demo-container">
                    <div class="demo-panel">
                        <h5>使用 watch（精確控制）</h5>
                        <div class="result">
                            <div class="display-value">
                                <strong>當前用戶：</strong>{{ watchUserData.name || '無' }}
                            </div>
                            <div class="display-value">
                                <strong>搜索結果：</strong>{{ watchSearchResults.length }} 筆
                            </div>
                            <div class="display-value">
                                <strong>API 呼叫次數：</strong>{{ watchApiCallCount }}
                            </div>
                        </div>
                        <div class="code-example">
                            <pre v-pre><code>// 分別控制不同 API 呼叫
watch(selectedUserId, async (newId) => {
  if (newId) {
    watchUserData.value = await fetchUser(newId)
  }
})

watch(searchQuery, async (newQuery) => {
  if (newQuery.length > 2) {
    watchSearchResults.value = await searchData(newQuery)
  }
}, { debounce: 300 })</code></pre>
                        </div>
                    </div>

                    <div class="demo-panel">
                        <h5>使用 watchEffect（自動追蹤）</h5>
                        <div class="result">
                            <div class="display-value">
                                <strong>綜合數據狀態：</strong>{{ effectDataStatus }}
                            </div>
                            <div class="display-value">
                                <strong>數據更新次數：</strong>{{ watchEffectDataCount }}
                            </div>
                        </div>
                        <div class="code-example">
                            <pre v-pre><code>// 自動追蹤所有相關變化
watchEffect(async () => {
  // 任何用到的響應式數據變化都會觸發
  if (selectedUserId.value && searchQuery.value) {
    effectDataStatus.value = '載入中...'
    // 同時獲取用戶和搜索數據
    const [user, results] = await Promise.all([
      fetchUser(selectedUserId.value),
      searchData(searchQuery.value)
    ])
    effectDataStatus.value = `${user.name}，找到 ${results.length} 筆 "${searchQuery.value}" 的結果`
  }
})</code></pre>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- 性能對比 -->
        <div class="demo-section">
            <h3>性能考量</h3>
            <div class="performance-grid">
                <div class="performance-card">
                    <h4>⚡ watch 特點</h4>
                    <ul>
                        <li><strong>惰性執行：</strong>只在數據變化時執行</li>
                        <li><strong>精確控制：</strong>只監聽指定的數據源</li>
                        <li><strong>較低開銷：</strong>不需要自動依賴追蹤</li>
                        <li><strong>適合：</strong>數據源明確且相對獨立的場景</li>
                    </ul>
                </div>
                <div class="performance-card">
                    <h4>🔄 watchEffect 特點</h4>
                    <ul>
                        <li><strong>立即執行：</strong>組件初始化時就執行一次</li>
                        <li><strong>自動追蹤：</strong>依賴收集有一定開銷</li>
                        <li><strong>重複執行：</strong>任何依賴變化都會觸發</li>
                        <li><strong>適合：</strong>需要響應多個數據源的副作用</li>
                    </ul>
                </div>
            </div>
        </div>

        <!-- 最佳實踐 -->
        <div class="demo-section">
            <h3>選擇建議與最佳實踐</h3>
            <div class="best-practices">
                <div class="practice-item good">
                    <h6>✅ 優先使用 watch 當：</h6>
                    <ul>
                        <li>需要對比變化前後的值</li>
                        <li>只需要監聽特定的數據源</li>
                        <li>需要延遲執行或條件執行</li>
                        <li>性能敏感的場景</li>
                    </ul>
                </div>
                <div class="practice-item good">
                    <h6>✅ 選擇 watchEffect 當：</h6>
                    <ul>
                        <li>需要響應多個相關的響應式數據</li>
                        <li>邏輯需要立即執行一次</li>
                        <li>不關心變化前的值</li>
                        <li>希望更簡潔的程式碼</li>
                    </ul>
                </div>
                <div class="practice-item caution">
                    <h6>⚠️ 注意事項：</h6>
                    <ul>
                        <li>避免在 watchEffect 中修改它正在追蹤的數據（無限循環）</li>
                        <li>複雜邏輯時，watch 通常更容易理解和維護</li>
                        <li>記得在適當時機停止偵聽器（組件卸載時）</li>
                        <li>大量數據變化時，考慮使用防抖（debounce）</li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, watch, watchEffect } from 'vue'

// 用戶資料驗證
const userEmail = ref('')
const userPassword = ref('')
const emailValidation = ref({ message: '請輸入郵件', class: 'info' })
const passwordValidation = ref({ message: '請輸入密碼', class: 'info' })
const effectFormValidation = ref({ isValid: false, message: '請填寫表單' })
const watchValidationCount = ref(0)
const watchEffectValidationCount = ref(0)

// 郵件驗證函數
const isValidEmail = (email) => {
    return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)
}

// watch 方式驗證
watch(userEmail, (newEmail) => {
    watchValidationCount.value++
    if (!newEmail) {
        emailValidation.value = { message: '請輸入郵件', class: 'info' }
    } else if (isValidEmail(newEmail)) {
        emailValidation.value = { message: '郵件格式正確', class: 'success' }
    } else {
        emailValidation.value = { message: '郵件格式錯誤', class: 'warning' }
    }
})

watch(userPassword, (newPassword) => {
    watchValidationCount.value++
    if (!newPassword) {
        passwordValidation.value = { message: '請輸入密碼', class: 'info' }
    } else if (newPassword.length < 6) {
        passwordValidation.value = { message: '密碼至少 6 個字符', class: 'warning' }
    } else {
        passwordValidation.value = { message: '密碼強度良好', class: 'success' }
    }
})

// watchEffect 方式驗證
watchEffect(() => {
    watchEffectValidationCount.value++
    const emailValid = userEmail.value && isValidEmail(userEmail.value)
    const passwordValid = userPassword.value && userPassword.value.length >= 6

    effectFormValidation.value = {
        isValid: emailValid && passwordValid,
        message: emailValid && passwordValid
            ? '表單填寫完整，可以提交'
            : '請完整填寫表單資料'
    }
})

// API 數據獲取模擬
const selectedUserId = ref('')
const searchQuery = ref('')
const watchUserData = ref({ name: '' })
const watchSearchResults = ref([])
const watchApiCallCount = ref(0)
const effectDataStatus = ref('請選擇用戶並輸入搜索內容')
const watchEffectDataCount = ref(0)

// 模擬 API 函數
const fetchUser = async (userId) => {
    await new Promise(resolve => setTimeout(resolve, 300))
    return { name: `用戶 ${userId}`, id: userId }
}

const searchData = async (query) => {
    await new Promise(resolve => setTimeout(resolve, 200))
    return Array.from({ length: Math.floor(Math.random() * 10) + 1 }, (_, i) => ({
        id: i,
        title: `${query} 相關結果 ${i + 1}`
    }))
}

// watch 方式處理 API
watch(selectedUserId, async (newId) => {
    if (newId) {
        watchApiCallCount.value++
        watchUserData.value = await fetchUser(newId)
    } else {
        watchUserData.value = { name: '' }
    }
})

watch(searchQuery, async (newQuery) => {
    if (newQuery && newQuery.length > 2) {
        watchApiCallCount.value++
        watchSearchResults.value = await searchData(newQuery)
    } else {
        watchSearchResults.value = []
    }
})

// watchEffect 方式處理
watchEffect(async () => {
    watchEffectDataCount.value++

    if (selectedUserId.value && searchQuery.value && searchQuery.value.length > 2) {
        effectDataStatus.value = '載入中...'
        try {
            const [user, results] = await Promise.all([
                fetchUser(selectedUserId.value),
                searchData(searchQuery.value)
            ])
            effectDataStatus.value = `${user.name}，找到 ${results.length} 筆 "${searchQuery.value}" 的結果`
        } catch {
            effectDataStatus.value = '載入失敗'
        }
    } else if (selectedUserId.value) {
        effectDataStatus.value = '請輸入搜索關鍵字（至少 3 個字符）'
    } else if (searchQuery.value) {
        effectDataStatus.value = '請選擇用戶'
    } else {
        effectDataStatus.value = '請選擇用戶並輸入搜索內容'
    }
})
</script>
