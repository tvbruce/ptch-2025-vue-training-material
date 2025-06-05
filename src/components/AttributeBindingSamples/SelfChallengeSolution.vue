<template>
    <div class="self-challenge">
        <h2>🎯 自我試煉解答 - 屬性綁定</h2>
        <p class="route-info">📍 路徑：/AttributeBindingSamples/SelfChallengeSolution.vue</p>
        <p class="description">
            ✅ <strong>完整解答：</strong>動態卡片組件屬性綁定完整實作範例
        </p>

        <div class="solution-overview">
            <h3>📋 解答概覽</h3>
            <div class="feature-list">
                <div class="feature-item completed">
                    <span class="icon">✅</span>
                    <span>基本屬性綁定（src、alt、href）</span>
                </div>
                <div class="feature-item completed">
                    <span class="icon">✅</span>
                    <span>動態 Class 綁定（物件語法、陣列語法）</span>
                </div>
                <div class="feature-item completed">
                    <span class="icon">✅</span>
                    <span>動態 Style 綁定（內聯樣式控制）</span>
                </div>
                <div class="feature-item completed">
                    <span class="icon">✅</span>
                    <span>條件屬性綁定（disabled、required）</span>
                </div>
                <div class="feature-item completed">
                    <span class="icon">✅</span>
                    <span>v-bind 物件語法批量綁定</span>
                </div>
                <div class="feature-item completed">
                    <span class="icon">✅</span>
                    <span>完整動態卡片組件</span>
                </div>
            </div>
        </div>

        <!-- 動態卡片展示區 -->
        <div class="card-showcase">
            <h3>🎨 動態卡片展示</h3>
            <div :class="cardClasses" :style="cardStyles" class="dynamic-card">
                <div class="card-header">
                    <img :src="cardImageSrc" :alt="selectedTheme" class="card-image">
                    <h4>{{ selectedTheme.toUpperCase() }} 主題卡片</h4>
                </div>

                <div class="card-body">
                    <p>這是一個動態卡片，展示了各種屬性綁定技巧。</p>
                    <a v-bind="linkAttributes" class="card-link">
                        {{ linkAttributes.title || '點擊查看更多' }}
                    </a>
                </div>

                <div class="card-footer">
                    <span class="status-indicator" :class="{ active: isActive }">
                        {{ isActive ? '啟用' : '停用' }}
                    </span>
                </div>
            </div>
        </div>

        <!-- 控制面板 -->
        <div class="control-panel">
            <h3>🎛️ 控制面板</h3>

            <!-- 主題選擇 -->
            <div class="control-group">
                <h4>主題選擇</h4>
                <div class="theme-selector">
                    <label v-for="theme in themes" :key="theme.value" class="theme-option"
                        :class="{ selected: selectedTheme === theme.value }">
                        <input type="radio" :value="theme.value" v-model="selectedTheme">
                        <span class="theme-preview" :style="{ backgroundColor: theme.color }"></span>
                        <span>{{ theme.label }}</span>
                    </label>
                </div>
            </div>

            <!-- 卡片狀態 -->
            <div class="control-group">
                <h4>卡片狀態</h4>
                <div class="status-controls">
                    <label class="checkbox-label">
                        <input type="checkbox" v-model="isActive">
                        啟用狀態
                    </label>
                    <label class="checkbox-label">
                        <input type="checkbox" v-model="isHighlighted">
                        高亮顯示
                    </label>
                    <label class="checkbox-label">
                        <input type="checkbox" v-model="isLoading">
                        載入狀態
                    </label>
                </div>
            </div>

            <!-- 樣式調整 -->
            <div class="control-group">
                <h4>樣式調整</h4>
                <div class="style-controls">
                    <div class="slider-control">
                        <label>背景顏色：</label>
                        <input type="color" v-model="customColor">
                    </div>

                    <div class="slider-control">
                        <label>邊框寬度：{{ borderWidth }}px</label>
                        <input type="range" min="0" max="10" v-model.number="borderWidth">
                    </div>

                    <div class="slider-control">
                        <label>透明度：{{ opacity }}%</label>
                        <input type="range" min="0" max="100" v-model.number="opacity">
                    </div>

                    <div class="slider-control">
                        <label>縮放：{{ scale }}</label>
                        <input type="range" min="0.5" max="2" step="0.1" v-model.number="scale">
                    </div>
                </div>
            </div>

            <!-- 連結設定 -->
            <div class="control-group">
                <h4>連結設定</h4>
                <div class="link-controls">
                    <input v-model="linkUrl" placeholder="連結網址" class="input-field">
                    <input v-model="linkTitle" placeholder="連結標題" class="input-field">
                    <label class="checkbox-label">
                        <input type="checkbox" v-model="openInNewTab">
                        在新視窗開啟
                    </label>
                </div>
            </div>
        </div>

        <!-- 表單驗證示例 -->
        <div class="form-demo">
            <h3>📝 表單屬性綁定示例</h3>
            <form class="demo-form">
                <div class="form-group">
                    <label>用戶名稱：</label>
                    <input v-bind="formFieldAttrs" v-model="formData.username" type="text" class="form-input">
                </div>

                <div class="form-group">
                    <label>電子郵件：</label>
                    <input v-model="formData.email" type="email" :disabled="isFormDisabled" :required="isRequired"
                        class="form-input">
                </div>

                <div class="form-controls">
                    <label class="checkbox-label">
                        <input type="checkbox" v-model="isFormDisabled">
                        禁用表單
                    </label>
                    <label class="checkbox-label">
                        <input type="checkbox" v-model="isRequired">
                        必填欄位
                    </label>
                </div>
            </form>
        </div>

        <!-- 綁定語法說明 -->
        <div class="syntax-demo">
            <h3>📚 綁定語法說明</h3>
            <div class="syntax-examples">
                <div class="syntax-card">
                    <h4>基本屬性綁定</h4>
                    <pre><code>&lt;!-- 完整語法 --&gt;
&lt;img v-bind:src="imageSrc" v-bind:alt="imageAlt"&gt;

&lt;!-- 簡寫語法 --&gt;
&lt;img :src="imageSrc" :alt="imageAlt"&gt;</code></pre>
                </div>

                <div class="syntax-card">
                    <h4>Class 綁定</h4>
                    <pre><code>&lt;!-- 物件語法 --&gt;
&lt;div :class="{ active: isActive, highlighted: isHighlighted }"&gt;

&lt;!-- 陣列語法 --&gt;
&lt;div :class="[baseClass, { extraClass: condition }]"&gt;</code></pre>
                </div>

                <div class="syntax-card">
                    <h4>Style 綁定</h4>
                    <pre><code>&lt;!-- 物件語法 --&gt;
&lt;div :style="{ color: textColor, fontSize: fontSize + 'px' }"&gt;

&lt;!-- 陣列語法 --&gt;
&lt;div :style="[baseStyles, extraStyles]"&gt;</code></pre>
                </div>

                <div class="syntax-card">
                    <h4>批量屬性綁定</h4>
                    <pre><code>&lt;!-- v-bind 物件語法 --&gt;
&lt;input v-bind="inputAttrs"&gt;

&lt;!-- 等同於 --&gt;
&lt;input
  :id="inputAttrs.id"
  :placeholder="inputAttrs.placeholder"
  :disabled="inputAttrs.disabled"
&gt;</code></pre>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, reactive, computed } from 'vue'

// ===== 基本響應式資料 =====
const selectedTheme = ref('nature')
const isActive = ref(true)
const isHighlighted = ref(false)
const isLoading = ref(false)

// 樣式控制
const customColor = ref('#4CAF50')
const borderWidth = ref(2)
const opacity = ref(100)
const scale = ref(1)

// 連結設定
const linkUrl = ref('https://vuejs.org')
const linkTitle = ref('Vue.js 官網')
const openInNewTab = ref(true)

// 表單設定
const isFormDisabled = ref(false)
const isRequired = ref(true)
const placeholderText = ref('請輸入用戶名稱')
const maxLength = ref(20)
const validationPattern = ref('[a-zA-Z0-9]+')

// 表單資料
const formData = reactive({
    username: '',
    email: ''
})

// 主題選項
const themes = [
    { value: 'nature', label: '自然', color: '#4CAF50' },
    { value: 'technology', label: '科技', color: '#2196F3' },
    { value: 'art', label: '藝術', color: '#E91E63' },
    { value: 'default', label: '預設', color: '#9E9E9E' }
]

// ===== 計算屬性 =====

// 1. 卡片圖片來源
const cardImageSrc = computed(() => {
    const imageMap = {
        'nature': 'https://via.placeholder.com/300x200/4CAF50/ffffff?text=Nature',
        'technology': 'https://via.placeholder.com/300x200/2196F3/ffffff?text=Tech',
        'art': 'https://via.placeholder.com/300x200/E91E63/ffffff?text=Art',
        'default': 'https://via.placeholder.com/300x200/9E9E9E/ffffff?text=Default'
    }
    return imageMap[selectedTheme.value] || imageMap.default
})

// 2. 卡片 CSS 類別
const cardClasses = computed(() => {
    return {
        'dynamic-card': true,
        [`theme-${selectedTheme.value}`]: true,
        'active': isActive.value,
        'highlighted': isHighlighted.value,
        'loading': isLoading.value
    }
})

// 3. 卡片內聯樣式
const cardStyles = computed(() => {
    return {
        backgroundColor: customColor.value,
        borderWidth: `${borderWidth.value}px`,
        opacity: opacity.value / 100,
        transform: `scale(${scale.value})`
    }
})

// 4. 連結屬性
const linkAttributes = computed(() => {
    const attrs = {
        href: linkUrl.value || '#',
        title: linkTitle.value
    }

    if (openInNewTab.value) {
        attrs.target = '_blank'
        attrs.rel = 'noopener noreferrer'
    }

    return attrs
})

// 5. 表單欄位屬性
const formFieldAttrs = computed(() => {
    const attrs = {
        placeholder: placeholderText.value,
        disabled: isFormDisabled.value
    }

    if (isRequired.value) {
        attrs.required = true
    }

    if (maxLength.value > 0) {
        attrs.maxlength = maxLength.value
    }

    if (validationPattern.value) {
        attrs.pattern = validationPattern.value
    }

    return attrs
})
</script>

<style scoped>
@import '@/assets/main.css';

.solution-overview {
    background: linear-gradient(135deg, #e3f2fd 0%, #f1f8e9 100%);
    padding: 1.5rem;
    border-radius: 8px;
    margin-bottom: 2rem;
    border: 2px solid #2196F3;
}

.feature-list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 0.5rem;
    margin-top: 1rem;
}

.feature-item {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.5rem;
}

.feature-item.completed .icon {
    color: #4CAF50;
    font-weight: bold;
}

/* 動態卡片樣式 */
.card-showcase {
    margin-bottom: 2rem;
}

.dynamic-card {
    max-width: 400px;
    margin: 1rem auto;
    border: 2px solid #ddd;
    border-radius: 8px;
    overflow: hidden;
    background: white;
    transition: all 0.3s ease;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.dynamic-card.active {
    box-shadow: 0 4px 16px rgba(0, 0, 0, 0.2);
}

.dynamic-card.highlighted {
    border-color: #FF9800;
    box-shadow: 0 0 20px rgba(255, 152, 0, 0.5);
}

.dynamic-card.loading {
    opacity: 0.7;
    pointer-events: none;
}

.dynamic-card.theme-nature {
    border-color: #4CAF50;
}

.dynamic-card.theme-technology {
    border-color: #2196F3;
}

.dynamic-card.theme-art {
    border-color: #E91E63;
}

.card-header {
    padding: 1rem;
    text-align: center;
}

.card-image {
    width: 100%;
    height: 150px;
    object-fit: cover;
    border-radius: 4px;
    margin-bottom: 0.5rem;
}

.card-body {
    padding: 1rem;
}

.card-link {
    display: inline-block;
    padding: 0.5rem 1rem;
    background: #007bff;
    color: white;
    text-decoration: none;
    border-radius: 4px;
    margin-top: 0.5rem;
    transition: background-color 0.2s;
}

.card-link:hover {
    background: #0056b3;
}

.card-footer {
    padding: 0.5rem 1rem;
    background: #f8f9fa;
    border-top: 1px solid #ddd;
}

.status-indicator {
    padding: 0.25rem 0.5rem;
    border-radius: 20px;
    font-size: 0.875rem;
    background: #6c757d;
    color: white;
}

.status-indicator.active {
    background: #28a745;
}

/* 控制面板樣式 */
.control-panel {
    background: #f8f9fa;
    padding: 1.5rem;
    border-radius: 8px;
    margin-bottom: 2rem;
}

.control-group {
    margin-bottom: 1.5rem;
    padding-bottom: 1rem;
    border-bottom: 1px solid #ddd;
}

.control-group:last-child {
    border-bottom: none;
}

.theme-selector {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
}

.theme-option {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.5rem;
    border: 2px solid transparent;
    border-radius: 8px;
    cursor: pointer;
    transition: border-color 0.2s;
}

.theme-option.selected {
    border-color: #007bff;
    background: rgba(0, 123, 255, 0.1);
}

.theme-option input[type="radio"] {
    display: none;
}

.theme-preview {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    border: 2px solid #ddd;
}

.status-controls,
.link-controls {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
}

.checkbox-label {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    cursor: pointer;
}

.style-controls {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
}

.slider-control {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}

.slider-control label {
    font-weight: 500;
    font-size: 0.9rem;
}

.slider-control input[type="range"] {
    width: 100%;
}

.input-field {
    padding: 0.5rem;
    border: 1px solid #ddd;
    border-radius: 4px;
    flex: 1;
    min-width: 150px;
}

/* 表單示例樣式 */
.form-demo {
    background: #fff;
    padding: 1.5rem;
    border-radius: 8px;
    border: 1px solid #ddd;
    margin-bottom: 2rem;
}

.demo-form {
    max-width: 500px;
}

.form-group {
    display: flex;
    align-items: center;
    gap: 1rem;
    margin-bottom: 1rem;
}

.form-group label {
    min-width: 100px;
    font-weight: 500;
}

.form-input {
    flex: 1;
    padding: 0.5rem;
    border: 1px solid #ddd;
    border-radius: 4px;
}

.form-input:disabled {
    background: #f8f9fa;
    color: #6c757d;
}

.form-controls {
    display: flex;
    gap: 1rem;
    margin-top: 1rem;
}

/* 語法說明樣式 */
.syntax-demo {
    background: #f8f9fa;
    padding: 1.5rem;
    border-radius: 8px;
}

.syntax-examples {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 1rem;
    margin-top: 1rem;
}

.syntax-card {
    background: white;
    padding: 1rem;
    border-radius: 8px;
    border: 1px solid #ddd;
}

.syntax-card h4 {
    color: #007bff;
    margin-bottom: 0.5rem;
}

.syntax-card pre {
    background: #f8f9fa;
    padding: 1rem;
    border-radius: 4px;
    overflow-x: auto;
    font-size: 0.875rem;
    margin: 0;
}

.syntax-card code {
    font-family: 'Courier New', monospace;
}
</style>
