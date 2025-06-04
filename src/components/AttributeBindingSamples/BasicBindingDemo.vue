<!-- components/AttributeBindingSamples/BasicBindingDemo.vue -->
<template>
  <div class="basic-binding-demo">
    <h2>基礎屬性綁定 (v-bind)</h2>
    <p class="route-info">📍 路徑：/AttributeBindingSamples/BasicBindingDemo.vue</p>

    <!-- 基本 v-bind 用法 -->
    <div class="demo-section">
      <h3>1. 基本 v-bind 語法</h3>
      <div class="controls">
        <input v-model="imageUrl" placeholder="輸入圖片網址" class="input-field">
        <input v-model="linkUrl" placeholder="輸入連結網址" class="input-field">
      </div>
      <div class="result">
        <!-- 完整語法 -->
        <div class="example-item">
          <h4>完整語法 v-bind:</h4>
          <img v-bind:src="imageUrl || defaultImage" v-bind:alt="imageAlt" class="demo-image">
          <a v-bind:href="linkUrl || '#'" v-bind:target="linkTarget" class="demo-link">
            {{ linkText }}
          </a>
        </div>

        <!-- 簡寫語法 -->
        <div class="example-item">
          <h4>簡寫語法 :</h4>
          <img :src="imageUrl || defaultImage" :alt="imageAlt" class="demo-image">
          <a :href="linkUrl || '#'" :target="linkTarget" class="demo-link">
            {{ linkText }}
          </a>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 完整語法 -->
&lt;img v-bind:src="imageUrl" v-bind:alt="imageAlt"&gt;
&lt;a v-bind:href="linkUrl" v-bind:target="linkTarget"&gt;連結&lt;/a&gt;

<!-- 簡寫語法 (推薦) -->
&lt;img :src="imageUrl" :alt="imageAlt"&gt;
&lt;a :href="linkUrl" :target="linkTarget"&gt;連結&lt;/a&gt;</code></pre>
      </div>
    </div>

    <!-- 屬性值為表達式 -->
    <div class="demo-section">
      <h3>2. 屬性值為 JavaScript 表達式</h3>
      <div class="controls">
        <input v-model="firstName" placeholder="名字" class="input-field">
        <input v-model="lastName" placeholder="姓氏" class="input-field">
        <input v-model.number="width" type="number" placeholder="寬度" class="input-field">
        <input v-model.number="height" type="number" placeholder="高度" class="input-field">
      </div>
      <div class="result">
        <div class="display-value">
          <!-- 字串拼接 -->
          <span :title="firstName + ' ' + lastName">
            滑鼠懸停看全名: {{ firstName }}
          </span>
        </div>
        <div class="display-value">
          <!-- 模板字串 -->
          <span :title="`完整姓名: ${firstName} ${lastName}`">
            模板字串: {{ firstName }}
          </span>
        </div>
        <div class="display-value">
          <!-- 數學運算 -->
          <div :style="{ width: width + 'px', height: height + 'px' }" class="size-box">
            尺寸: {{ width }} x {{ height }}
          </div>
        </div>
        <div class="display-value">
          <!-- 條件表達式 -->
          <button :disabled="!firstName || !lastName" class="demo-button">
            {{ firstName && lastName ? '提交' : '請填寫姓名' }}
          </button>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 字串拼接 -->
&lt;span :title="firstName + ' ' + lastName"&gt;

<!-- 模板字串 -->
&lt;span :title="`完整姓名: ${firstName} ${lastName}`"&gt;

<!-- 數學運算 -->
&lt;div :style="{ width: width + 'px', height: height + 'px' }"&gt;

<!-- 條件表達式 -->
&lt;button :disabled="!firstName || !lastName"&gt;</code></pre>
      </div>
    </div>

    <!-- 布林屬性 -->
    <div class="demo-section">
      <h3>3. 布林屬性綁定</h3>
      <div class="controls">
        <label class="checkbox-label">
          <input type="checkbox" v-model="isDisabled">
          按鈕禁用
        </label>
        <label class="checkbox-label">
          <input type="checkbox" v-model="isRequired">
          必填欄位
        </label>
        <label class="checkbox-label">
          <input type="checkbox" v-model="isChecked">
          預設勾選
        </label>
        <label class="checkbox-label">
          <input type="checkbox" v-model="isHidden">
          隱藏元素
        </label>
      </div>
      <div class="result">
        <div class="form-example">
          <input :disabled="isDisabled" :required="isRequired" placeholder="測試輸入框" class="input-field">
          <button :disabled="isDisabled" class="demo-button">
            測試按鈕
          </button>
          <label class="checkbox-label">
            <input type="checkbox" :checked="isChecked" :disabled="isDisabled">
            測試選項
          </label>
          <div :hidden="isHidden" class="hidden-content">
            這是可以隱藏的內容
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 布林屬性：true 時存在，false 時移除 -->
&lt;input :disabled="isDisabled"&gt;
&lt;input :required="isRequired"&gt;
&lt;input :checked="isChecked"&gt;
&lt;div :hidden="isHidden"&gt;內容&lt;/div&gt;

// 當值為 falsy 時，屬性會被移除
// 當值為 truthy 時，屬性會被添加</code></pre>
      </div>
    </div>

    <!-- 多個屬性綁定 -->
    <div class="demo-section">
      <h3>4. 綁定多個屬性</h3>
      <div class="controls">
        <select v-model="selectedTheme" class="select-field">
          <option value="light">淺色主題</option>
          <option value="dark">深色主題</option>
          <option value="colorful">彩色主題</option>
        </select>
      </div>
      <div class="result">
        <div v-bind="themeAttributes" class="theme-box">
          <h4>{{ themeAttributes.title }}</h4>
          <p>這是一個使用 v-bind 綁定多個屬性的範例</p>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 使用物件綁定多個屬性
const themeAttributes = computed(() => {
  const themes = {
    light: {
      title: '淺色主題',
      style: 'background: #f8f9fa; color: #333;'
    },
    dark: {
      title: '深色主題',
      style: 'background: #2c3e50; color: #ecf0f1;'
    },
    colorful: {
      title: '彩色主題',
      style: 'background: linear-gradient(45deg, #ff6b6b, #4ecdc4);'
    }
  }
  return themes[selectedTheme.value]
})

&lt;div v-bind="themeAttributes"&gt;內容&lt;/div&gt;</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 基本綁定
const imageUrl = ref('')
const linkUrl = ref('')
const defaultImage = 'https://picsum.photos/150/100'

const imageAlt = ref('示範圖片')
const linkTarget = ref('_blank')
const linkText = ref('示範連結')

// 表達式綁定
const firstName = ref('')
const lastName = ref('')
const width = ref(200)
const height = ref(100)

// 布林屬性
const isDisabled = ref(false)
const isRequired = ref(false)
const isChecked = ref(false)
const isHidden = ref(false)

// 多個屬性綁定
const selectedTheme = ref('light')

const themeAttributes = computed(() => {
  const themes = {
    light: {
      title: '淺色主題',
      style: 'background: #f8f9fa; color: #333; padding: 20px; border-radius: 8px; border: 2px solid #dee2e6;'
    },
    dark: {
      title: '深色主題',
      style: 'background: #2c3e50; color: #ecf0f1; padding: 20px; border-radius: 8px; border: 2px solid #34495e;'
    },
    colorful: {
      title: '彩色主題',
      style: 'background: linear-gradient(45deg, #ff6b6b, #4ecdc4); color: white; padding: 20px; border-radius: 8px; border: 2px solid #ff6b6b;'
    }
  }
  return themes[selectedTheme.value]
})
</script>

<style scoped>
/* 樣式已在 src/assets/main.css 中定義 */
</style>
