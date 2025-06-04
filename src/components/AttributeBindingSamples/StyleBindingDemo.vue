<!-- components/AttributeBindingSamples/StyleBindingDemo.vue -->
<template>
  <div class="style-binding-demo">
    <h2>Style 綁定 (:style)</h2>
    <p class="route-info">📍 路徑：/AttributeBindingSamples/StyleBindingDemo.vue</p>

    <!-- 物件語法 -->
    <div class="demo-section">
      <h3>1. 物件語法</h3>
      <div class="controls">
        <input v-model="backgroundColor" type="color" class="color-input">
        <label>背景色</label>

        <input v-model="textColor" type="color" class="color-input">
        <label>文字色</label>

        <input v-model.number="fontSize" type="range" min="12" max="36" class="range-input">
        <label>字體大小: {{ fontSize }}px</label>

        <input v-model.number="padding" type="range" min="10" max="50" class="range-input">
        <label>內距: {{ padding }}px</label>
      </div>
      <div class="result">
        <div class="example-item">
          <h4>基本物件語法：</h4>
          <div :style="{
            backgroundColor: backgroundColor,
            color: textColor,
            fontSize: fontSize + 'px',
            padding: padding + 'px'
          }" class="demo-box">
            我是樣式測試元素
          </div>
        </div>

        <div class="example-item">
          <h4>使用計算屬性：</h4>
          <div :style="computedStyles" class="demo-box">
            我使用計算屬性
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 基本物件語法 -->
&lt;div :style="{
  backgroundColor: backgroundColor,
  color: textColor,
  fontSize: fontSize + 'px',
  padding: padding + 'px'
}"&gt;

<!-- 使用計算屬性 -->
const computedStyles = computed(() => ({
  backgroundColor: backgroundColor.value,
  color: textColor.value,
  fontSize: fontSize.value + 'px',
  padding: padding.value + 'px',
  borderRadius: '8px',
  transition: 'all 0.3s ease'
}))</code></pre>
      </div>
    </div>

    <!-- 陣列語法 -->
    <div class="demo-section">
      <h3>2. 陣列語法</h3>
      <div class="controls">
        <label class="checkbox-label">
          <input type="checkbox" v-model="applyBaseStyles">
          基礎樣式
        </label>
        <label class="checkbox-label">
          <input type="checkbox" v-model="applyThemeStyles">
          主題樣式
        </label>
        <label class="checkbox-label">
          <input type="checkbox" v-model="applyAnimationStyles">
          動畫樣式
        </label>
      </div>
      <div class="result">
        <div class="example-item">
          <h4>陣列語法：</h4>
          <div :style="[
            applyBaseStyles ? baseStyles : {},
            applyThemeStyles ? themeStyles : {},
            applyAnimationStyles ? animationStyles : {}
          ]" class="demo-box">
            陣列樣式範例
          </div>
        </div>

        <div class="example-item">
          <h4>使用計算屬性陣列：</h4>
          <div :style="arrayStyles" class="demo-box">
            計算屬性陣列
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 陣列語法 -->
&lt;div :style="[baseStyles, themeStyles, animationStyles]"&gt;

<!-- 條件式陣列 -->
&lt;div :style="[
  applyBaseStyles ? baseStyles : {},
  applyThemeStyles ? themeStyles : {}
]"&gt;

// 樣式物件
const baseStyles = {
  padding: '20px',
  borderRadius: '8px',
  textAlign: 'center'
}

const themeStyles = {
  background: 'linear-gradient(45deg, #667eea 0%, #764ba2 100%)',
  color: 'white'
}</code></pre>
      </div>
    </div>

    <!-- 動態樣式 -->
    <div class="demo-section">
      <h3>3. 動態樣式效果</h3>
      <div class="controls">
        <button @click="startAnimation" class="btn btn-primary">
          {{ isAnimating ? '停止動畫' : '開始動畫' }}
        </button>
        <button @click="randomizeStyles" class="btn btn-secondary">
          隨機樣式
        </button>
        <button @click="resetStyles" class="btn btn-warning">
          重置樣式
        </button>
      </div>
      <div class="result">
        <div class="animation-container">
          <div :style="dynamicStyles" class="animated-element">
            <h4>動態樣式</h4>
            <p>我會動態改變樣式</p>
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 動態樣式
const dynamicStyles = computed(() => ({
  transform: `rotate(${rotation.value}deg) scale(${scale.value})`,
  backgroundColor: `hsl(${hue.value}, 70%, 60%)`,
  borderRadius: borderRadius.value + 'px',
  transition: isAnimating.value ? 'none' : 'all 0.5s ease'
}))

// 動畫控制
const startAnimation = () => {
  if (isAnimating.value) {
    clearInterval(animationTimer)
    isAnimating.value = false
  } else {
    isAnimating.value = true
    animationTimer = setInterval(() => {
      rotation.value = (rotation.value + 5) % 360
      hue.value = (hue.value + 2) % 360
      scale.value = 0.8 + Math.sin(Date.now() / 1000) * 0.3
    }, 50)
  }
}</code></pre>
      </div>
    </div>

    <!-- CSS 變數綁定 -->
    <div class="demo-section">
      <h3>4. CSS 變數綁定</h3>
      <div class="controls">
        <input v-model="primaryColor" type="color" class="color-input">
        <label>主色調</label>

        <input v-model="secondaryColor" type="color" class="color-input">
        <label>次色調</label>

        <input v-model.number="borderWidth" type="range" min="1" max="10" class="range-input">
        <label>邊框寬度: {{ borderWidth }}px</label>
      </div>
      <div class="result">
        <div :style="cssVariables" class="css-variables-demo">
          <div class="card">
            <h4>CSS 變數範例</h4>
            <p>這個卡片使用 CSS 變數來控制樣式</p>
            <button class="card-button">按鈕</button>
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// CSS 變數綁定
const cssVariables = computed(() => ({
  '--primary-color': primaryColor.value,
  '--secondary-color': secondaryColor.value,
  '--border-width': borderWidth.value + 'px'
}))

/* CSS 中使用變數 */
.css-variables-demo {
  --primary-color: #3498db;
  --secondary-color: #e74c3c;
  --border-width: 2px;
}

.card {
  border: var(--border-width) solid var(--primary-color);
  background: var(--secondary-color);
}</code></pre>
      </div>
    </div>

    <!-- 響應式樣式 -->
    <div class="demo-section">
      <h3>5. 響應式樣式</h3>
      <div class="controls">
        <input v-model.number="containerWidth" type="range" min="200" max="800" class="range-input">
        <label>容器寬度: {{ containerWidth }}px</label>

        <select v-model="layoutMode" class="select-field">
          <option value="horizontal">水平佈局</option>
          <option value="vertical">垂直佈局</option>
          <option value="grid">網格佈局</option>
        </select>
      </div>
      <div class="result">
        <div :style="responsiveContainerStyles" class="responsive-container">
          <div v-for="item in 6" :key="item" :style="responsiveItemStyles" class="responsive-item">
            項目 {{ item }}
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 響應式樣式
const responsiveContainerStyles = computed(() => ({
  width: containerWidth.value + 'px',
  display: layoutMode.value === 'grid' ? 'grid' : 'flex',
  flexDirection: layoutMode.value === 'vertical' ? 'column' : 'row',
  gridTemplateColumns: layoutMode.value === 'grid' ? 'repeat(auto-fit, minmax(100px, 1fr))' : 'none',
  gap: '10px',
  padding: '20px',
  border: '2px solid #ddd',
  borderRadius: '8px',
  backgroundColor: '#f8f9fa',
  margin: '0 auto',
  transition: 'all 0.3s ease'
}))

const responsiveItemStyles = computed(() => {
  const baseStyles = {
    padding: '15px',
    backgroundColor: '#ffffff',
    borderRadius: '4px',
    textAlign: 'center',
    border: '1px solid #dee2e6',
    fontWeight: '500',
    transition: 'all 0.3s ease'
  }

  if (containerWidth.value < 400) {
    baseStyles.fontSize = '12px'
    baseStyles.padding = '10px'
  } else if (containerWidth.value < 600) {
    baseStyles.fontSize = '14px'
  } else {
    baseStyles.fontSize = '16px'
  }

  return baseStyles
})</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onUnmounted } from 'vue'

// 物件語法
const backgroundColor = ref('#3498db')
const textColor = ref('#ffffff')
const fontSize = ref(16)
const padding = ref(20)

const computedStyles = computed(() => ({
  backgroundColor: backgroundColor.value,
  color: textColor.value,
  fontSize: fontSize.value + 'px',
  padding: padding.value + 'px',
  borderRadius: '8px',
  transition: 'all 0.3s ease',
  textAlign: 'center',
  fontWeight: '500'
}))

// 陣列語法
const applyBaseStyles = ref(true)
const applyThemeStyles = ref(true)
const applyAnimationStyles = ref(false)

const baseStyles = {
  padding: '20px',
  borderRadius: '8px',
  textAlign: 'center',
  fontWeight: '500'
}

const themeStyles = {
  background: 'linear-gradient(45deg, #667eea 0%, #764ba2 100%)',
  color: 'white',
  border: '2px solid #667eea'
}

const animationStyles = {
  transform: 'scale(1.05)',
  boxShadow: '0 4px 15px rgba(102, 126, 234, 0.4)',
  transition: 'all 0.3s ease'
}

const arrayStyles = computed(() => {
  const styles = []
  if (applyBaseStyles.value) styles.push(baseStyles)
  if (applyThemeStyles.value) styles.push(themeStyles)
  if (applyAnimationStyles.value) styles.push(animationStyles)
  return styles
})

// 動態樣式
const isAnimating = ref(false)
const rotation = ref(0)
const scale = ref(1)
const hue = ref(200)
const borderRadius = ref(8)
let animationTimer = null

const dynamicStyles = computed(() => ({
  transform: `rotate(${rotation.value}deg) scale(${scale.value})`,
  backgroundColor: `hsl(${hue.value}, 70%, 60%)`,
  borderRadius: borderRadius.value + 'px',
  transition: isAnimating.value ? 'none' : 'all 0.5s ease',
  padding: '30px',
  textAlign: 'center',
  color: 'white',
  fontWeight: 'bold',
  border: '3px solid white',
  boxShadow: '0 4px 15px rgba(0,0,0,0.2)'
}))

// CSS 變數
const primaryColor = ref('#3498db')
const secondaryColor = ref('#ecf0f1')
const borderWidth = ref(2)

const cssVariables = computed(() => ({
  '--primary-color': primaryColor.value,
  '--secondary-color': secondaryColor.value,
  '--border-width': borderWidth.value + 'px'
}))

// 響應式樣式
const containerWidth = ref(600)
const layoutMode = ref('horizontal')

const responsiveContainerStyles = computed(() => ({
  width: containerWidth.value + 'px',
  display: layoutMode.value === 'grid' ? 'grid' : 'flex',
  flexDirection: layoutMode.value === 'vertical' ? 'column' : 'row',
  gridTemplateColumns: layoutMode.value === 'grid' ? 'repeat(auto-fit, minmax(100px, 1fr))' : 'none',
  gap: '10px',
  padding: '20px',
  border: '2px solid #ddd',
  borderRadius: '8px',
  backgroundColor: '#f8f9fa',
  margin: '0 auto',
  transition: 'all 0.3s ease'
}))

const responsiveItemStyles = computed(() => {
  const baseStyles = {
    padding: '15px',
    backgroundColor: '#ffffff',
    borderRadius: '4px',
    textAlign: 'center',
    border: '1px solid #dee2e6',
    fontWeight: '500',
    transition: 'all 0.3s ease'
  }

  if (containerWidth.value < 400) {
    baseStyles.fontSize = '12px'
    baseStyles.padding = '10px'
  } else if (containerWidth.value < 600) {
    baseStyles.fontSize = '14px'
  } else {
    baseStyles.fontSize = '16px'
  }

  return baseStyles
})

// 方法
const startAnimation = () => {
  if (isAnimating.value) {
    clearInterval(animationTimer)
    isAnimating.value = false
  } else {
    isAnimating.value = true
    animationTimer = setInterval(() => {
      rotation.value = (rotation.value + 5) % 360
      hue.value = (hue.value + 2) % 360
      scale.value = 0.8 + Math.sin(Date.now() / 1000) * 0.3
      borderRadius.value = 8 + Math.sin(Date.now() / 500) * 20
    }, 50)
  }
}

const randomizeStyles = () => {
  backgroundColor.value = `hsl(${Math.random() * 360}, 70%, 60%)`
  textColor.value = Math.random() > 0.5 ? '#ffffff' : '#000000'
  fontSize.value = Math.floor(Math.random() * 25) + 12
  padding.value = Math.floor(Math.random() * 41) + 10

  rotation.value = Math.random() * 360
  scale.value = 0.5 + Math.random() * 1
  hue.value = Math.random() * 360
  borderRadius.value = Math.random() * 50
}

const resetStyles = () => {
  backgroundColor.value = '#3498db'
  textColor.value = '#ffffff'
  fontSize.value = 16
  padding.value = 20

  rotation.value = 0
  scale.value = 1
  hue.value = 200
  borderRadius.value = 8
}

// 清理
onUnmounted(() => {
  if (animationTimer) {
    clearInterval(animationTimer)
  }
})
</script>

<style scoped>
/* 樣式已在 src/assets/main.css 中定義 */
</style>
