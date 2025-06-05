<template>
  <div class="vue2-vs-vue3-demo">
    <h2>Vue2 vs Vue3 開發方式對比</h2>
    <p class="route-info">📍 路徑：/ComponentSamples/Vue2Vs3ComparisonDemo.vue</p>

    <!-- 組件定義語法對比 -->
    <div class="demo-section">
      <h3>1. 組件定義語法對比</h3>
      <div class="comparison-grid">
        <div class="comparison-card vue2-card">
          <h4>Vue 2 - Options API</h4>
          <div class="code-example">
            <pre v-pre><code>export default {
  name: 'MyComponent',
  data() {
    return {
      message: 'Hello Vue 2',
      count: 0
    }
  },
  props: {
    title: String,
    isActive: Boolean
  },
  computed: {
    displayMessage() {
      return this.title + ': ' + this.message
    }
  },
  methods: {
    increment() {
      this.count++
    }
  },
  created() {
    console.log('組件已創建')
  }
}</code></pre>
          </div>
        </div>
        <div class="comparison-card vue3-card">
          <h4>Vue 3 - Composition API</h4>
          <div class="code-example">
            <pre v-pre><code>&lt;script setup&gt;
import { ref, computed, onMounted } from 'vue'

const props = defineProps({
  title: String,
  isActive: Boolean
})

const message = ref('Hello Vue 3')
const count = ref(0)

const displayMessage = computed(() => {
  return props.title + ': ' + message.value
})

const increment = () => {
  count.value++
}

onMounted(() => {
  console.log('組件已掛載')
})
&lt;/script&gt;</code></pre>
          </div>
        </div>
      </div>
    </div>

    <!-- 響應式數據對比 -->
    <div class="demo-section">
      <h3>2. 響應式數據宣告</h3>
      <div class="comparison-grid">
        <div class="comparison-card vue2-card">
          <h4>Vue 2</h4>
          <div class="code-example">
            <pre v-pre><code>export default {
  data() {
    return {
      // 基本類型
      userName: '',
      age: 0,
      isActive: false,

      // 物件類型
      user: {
        name: '',
        email: ''
      },

      // 陣列類型
      skills: []
    }
  }
}</code></pre>
          </div>
        </div>
        <div class="comparison-card vue3-card">
          <h4>Vue 3</h4>
          <div class="code-example">
            <pre v-pre><code>&lt;script setup&gt;
import { ref, reactive } from 'vue'

// 基本類型使用 ref
const userName = ref('')
const age = ref(0)
const isActive = ref(false)

// 物件類型可使用 reactive
const user = reactive({
  name: '',
  email: ''
})

// 陣列類型 - 推薦使用 ref
const skills = ref([])
// 或使用 reactive (較少用)
const skillsReactive = reactive([])
&lt;/script&gt;</code></pre>
          </div>
        </div>
      </div>
      <div class="demo-container">
        <h4>實際演示</h4>
        <div class="controls">
          <input v-model="demoName" placeholder="輸入姓名" class="input-field">
          <input v-model.number="demoAge" type="number" placeholder="輸入年齡" class="input-field">
          <button @click="addSkill" class="btn btn-primary">新增技能</button>
        </div>
        <div class="result">
          <div class="display-value">
            姓名: {{ demoName || '未設定' }}
          </div>
          <div class="display-value">
            年齡: {{ demoAge || '未設定' }}
          </div>
          <div class="display-value">
            技能列表: {{ demoSkills.join(', ') || '無' }}
          </div>
        </div>
      </div>
    </div>

    <!-- 計算屬性對比 -->
    <div class="demo-section">
      <h3>3. 計算屬性 (Computed)</h3>
      <div class="comparison-grid">
        <div class="comparison-card vue2-card">
          <h4>Vue 2</h4>
          <div class="code-example">
            <pre v-pre><code>export default {
  data() {
    return {
      firstName: '',
      lastName: ''
    }
  },
  computed: {
    fullName() {
      return this.firstName + ' ' + this.lastName
    },
    // 可寫計算屬性
    fullNameWritable: {
      get() {
        return this.firstName + ' ' + this.lastName
      },
      set(value) {
        const names = value.split(' ')
        this.firstName = names[0]
        this.lastName = names[1] || ''
      }
    }
  }
}</code></pre>
          </div>
        </div>
        <div class="comparison-card vue3-card">
          <h4>Vue 3</h4>
          <div class="code-example">
            <pre v-pre><code>&lt;script setup&gt;
import { ref, computed } from 'vue'

const firstName = ref('')
const lastName = ref('')

const fullName = computed(() => {
  return firstName.value + ' ' + lastName.value
})

// 可寫計算屬性
const fullNameWritable = computed({
  get: () => firstName.value + ' ' + lastName.value,
  set: (value) => {
    const names = value.split(' ')
    firstName.value = names[0]
    lastName.value = names[1] || ''
  }
})
&lt;/script&gt;</code></pre>
          </div>
        </div>
      </div>
      <div class="demo-container">
        <h4>計算屬性演示</h4>
        <div class="controls">
          <input v-model="firstName" placeholder="名字" class="input-field">
          <input v-model="lastName" placeholder="姓氏" class="input-field">
        </div>
        <div class="result">
          <div class="display-value">
            完整姓名: {{ fullName }}
          </div>
          <div class="display-value">
            姓名長度: {{ fullName.length }} 個字符
          </div>
        </div>
      </div>
    </div>

    <!-- 生命週期對比 -->
    <div class="demo-section">
      <h3>4. 生命週期鉤子</h3>
      <div class="comparison-grid">
        <div class="comparison-card vue2-card">
          <h4>Vue 2</h4>
          <div class="code-example">
            <pre v-pre><code>export default {
  beforeCreate() {
    console.log('beforeCreate')
  },
  created() {
    console.log('created')
  },
  beforeMount() {
    console.log('beforeMount')
  },
  mounted() {
    console.log('mounted')
  },
  beforeUpdate() {
    console.log('beforeUpdate')
  },
  updated() {
    console.log('updated')
  },
  beforeDestroy() {
    console.log('beforeDestroy')
  },
  destroyed() {
    console.log('destroyed')
  }
}</code></pre>
          </div>
        </div>
        <div class="comparison-card vue3-card">
          <h4>Vue 3</h4>
          <div class="code-example">
            <pre v-pre><code>&lt;script setup&gt;
import {
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted
} from 'vue'

// setup() 相當於 beforeCreate + created

onBeforeMount(() => {
  console.log('onBeforeMount')
})

onMounted(() => {
  console.log('onMounted')
})

onBeforeUpdate(() => {
  console.log('onBeforeUpdate')
})

onUpdated(() => {
  console.log('onUpdated')
})

onBeforeUnmount(() => {
  console.log('onBeforeUnmount')
})

onUnmounted(() => {
  console.log('onUnmounted')
})
&lt;/script&gt;</code></pre>
          </div>
        </div>
      </div>
      <div class="info-box">
        <h4>生命週期對照表</h4>
        <ul>
          <li><strong>beforeCreate / created</strong> → <strong>setup()</strong></li>
          <li><strong>beforeMount</strong> → <strong>onBeforeMount</strong></li>
          <li><strong>mounted</strong> → <strong>onMounted</strong></li>
          <li><strong>beforeUpdate</strong> → <strong>onBeforeUpdate</strong></li>
          <li><strong>updated</strong> → <strong>onUpdated</strong></li>
          <li><strong>beforeDestroy</strong> → <strong>onBeforeUnmount</strong></li>
          <li><strong>destroyed</strong> → <strong>onUnmounted</strong></li>
        </ul>
      </div>
    </div>

    <!-- 事件處理對比 -->
    <div class="demo-section">
      <h3>5. 事件處理與方法</h3>
      <div class="comparison-grid">
        <div class="comparison-card vue2-card">
          <h4>Vue 2</h4>
          <div class="code-example">
            <pre v-pre><code>export default {
  data() {
    return {
      counter: 0,
      message: ''
    }
  },
  methods: {
    increment() {
      this.counter++
    },
    handleInput(event) {
      this.message = event.target.value
    },
    submitForm() {
      this.$emit('submit', {
        counter: this.counter,
        message: this.message
      })
    }
  }
}</code></pre>
          </div>
        </div>
        <div class="comparison-card vue3-card">
          <h4>Vue 3</h4>
          <div class="code-example">
            <pre v-pre><code>&lt;script setup&gt;
import { ref } from 'vue'

const emit = defineEmits(['submit'])

const counter = ref(0)
const message = ref('')

const increment = () => {
  counter.value++
}

const handleInput = (event) => {
  message.value = event.target.value
}

const submitForm = () => {
  emit('submit', {
    counter: counter.value,
    message: message.value
  })
}
&lt;/script&gt;</code></pre>
          </div>
        </div>
      </div>
      <div class="demo-container">
        <h4>事件處理演示</h4>
        <div class="controls">
          <button @click="increment" class="btn btn-primary">點擊計數: {{ demoCounter }}</button>
          <input @input="handleDemoInput" placeholder="輸入訊息" class="input-field">
        </div>
        <div class="result">
          <div class="display-value">
            當前計數: {{ demoCounter }}
          </div>
          <div class="display-value">
            輸入內容: {{ demoMessage }}
          </div>
        </div>
      </div>
    </div>

    <!-- Watch 監聽對比 -->
    <div class="demo-section">
      <h3>6. 監聽器 (Watch)</h3>
      <div class="comparison-grid">
        <div class="comparison-card vue2-card">
          <h4>Vue 2</h4>
          <div class="code-example">
            <pre v-pre><code>export default {
  data() {
    return {
      searchText: '',
      user: {
        name: '',
        age: 0
      }
    }
  },
  watch: {
    // 簡單監聽
    searchText(newVal, oldVal) {
      console.log('搜尋文字變化:', oldVal, '->', newVal)
    },

    // 深度監聽
    user: {
      handler(newVal, oldVal) {
        console.log('用戶資料變化:', newVal)
      },
      deep: true
    },

    // 立即執行
    'user.name': {
      handler(newVal) {
        console.log('用戶名稱:', newVal)
      },
      immediate: true
    }
  }
}</code></pre>
          </div>
        </div>
        <div class="comparison-card vue3-card">
          <h4>Vue 3</h4>
          <div class="code-example">
            <pre v-pre><code>&lt;script setup&gt;
import { ref, reactive, watch, watchEffect } from 'vue'

const searchText = ref('')
const user = reactive({
  name: '',
  age: 0
})

// 簡單監聽
watch(searchText, (newVal, oldVal) => {
  console.log('搜尋文字變化:', oldVal, '->', newVal)
})

// 深度監聽
watch(user, (newVal, oldVal) => {
  console.log('用戶資料變化:', newVal)
}, { deep: true })

    // 監聽深層屬性
    watch(() => user.name, (newVal, oldVal) => {
      console.log('用戶名稱變化:', oldVal, '->', newVal)
    }, { immediate: true })

// watchEffect 自動追蹤依賴
watchEffect(() => {
  console.log('自動監聽:', searchText.value, user.name)
})
&lt;/script&gt;</code></pre>
          </div>
        </div>
      </div>
    </div>

    <!-- 引用其他函數與元件對比 -->
    <div class="demo-section">
      <h3>7. 引用其他函數與元件</h3>
      <div class="comparison-grid">
        <div class="comparison-card vue2-card">
          <h4>Vue 2 - Options API</h4>
          <div class="code-example">
            <pre v-pre><code>// utils.js - 工具函數
export const formatDate = (date) => {
  return date.toLocaleDateString('zh-TW')
}

export const validateEmail = (email) => {
  return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)
}

// MyComponent.vue
import { formatDate, validateEmail } from '@/utils'
import OtherComponent from '@/components/OtherComponent.vue'

export default {
  name: 'MyComponent',
  components: {
    OtherComponent
  },
  data() {
    return {
      email: '',
      currentDate: new Date()
    }
  },
  computed: {
    formattedDate() {
      return formatDate(this.currentDate)
    },
    isEmailValid() {
      return validateEmail(this.email)
    }
  },
  methods: {
    handleSubmit() {
      if (this.isEmailValid) {
        console.log('提交成功')
      }
    }
  }
}</code></pre>
          </div>
        </div>
        <div class="comparison-card vue3-card">
          <h4>Vue 3 - Composition API</h4>
          <div class="code-example">
            <pre v-pre><code>// composables/useValidation.js
import { computed } from 'vue'

export function useValidation() {
  const validateEmail = (email) => {
    return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)
  }

  const validateRequired = (value) => {
    return value && value.trim().length > 0
  }

  return {
    validateEmail,
    validateRequired
  }
}

// composables/useDate.js
export function useDate() {
  const formatDate = (date) => {
    return date.toLocaleDateString('zh-TW')
  }

  const getCurrentDate = () => {
    return new Date()
  }

  return {
    formatDate,
    getCurrentDate
  }
}

// MyComponent.vue
&lt;script setup&gt;
import { ref, computed } from 'vue'
import { useValidation } from '@/composables/useValidation'
import { useDate } from '@/composables/useDate'
import OtherComponent from '@/components/OtherComponent.vue'

const { validateEmail } = useValidation()
const { formatDate, getCurrentDate } = useDate()

const email = ref('')
const currentDate = ref(getCurrentDate())

const formattedDate = computed(() => {
  return formatDate(currentDate.value)
})

const isEmailValid = computed(() => {
  return validateEmail(email.value)
})

const handleSubmit = () => {
  if (isEmailValid.value) {
    console.log('提交成功')
  }
}
&lt;/script&gt;</code></pre>
          </div>
        </div>
      </div>
    </div>

    <!-- Mixins vs Composables -->
    <div class="demo-section">
      <h3>8. 邏輯複用：Mixins vs Composables</h3>
      <div class="comparison-grid">
        <div class="comparison-card vue2-card">
          <h4>Vue 2 - Mixins</h4>
          <div class="code-example">
            <pre v-pre><code>// mixins/counterMixin.js
export const counterMixin = {
  data() {
    return {
      count: 0
    }
  },
  methods: {
    increment() {
      this.count++
    },
    decrement() {
      this.count--
    },
    reset() {
      this.count = 0
    }
  }
}

// 使用 mixin
import { counterMixin } from '@/mixins/counterMixin'

export default {
  mixins: [counterMixin],
  data() {
    return {
      title: '計數器組件'
    }
  },
  computed: {
    displayText() {
      return `${this.title}: ${this.count}`
    }
  }
}</code></pre>
          </div>
        </div>
        <div class="comparison-card vue3-card">
          <h4>Vue 3 - Composables</h4>
          <div class="code-example">
            <pre v-pre><code>// composables/useCounter.js
import { ref } from 'vue'

export function useCounter(initialValue = 0) {
  const count = ref(initialValue)

  const increment = () => {
    count.value++
  }

  const decrement = () => {
    count.value--
  }

  const reset = () => {
    count.value = initialValue
  }

  return {
    count,
    increment,
    decrement,
    reset
  }
}

// 使用 composable
&lt;script setup&gt;
import { ref, computed } from 'vue'
import { useCounter } from '@/composables/useCounter'

const title = ref('計數器組件')
const { count, increment, decrement, reset } = useCounter(10)

const displayText = computed(() => {
  return `${title.value}: ${count.value}`
})
&lt;/script&gt;</code></pre>
          </div>
        </div>
      </div>
      <div class="demo-container">
        <h4>Composable 實際演示</h4>
        <div class="controls">
          <button @click="composableIncrement" class="btn btn-primary">增加</button>
          <button @click="composableDecrement" class="btn btn-secondary">減少</button>
          <button @click="composableReset" class="btn btn-danger">重置</button>
        </div>
        <div class="result">
          <div class="display-value">
            計數值: {{ composableCount }}
          </div>
          <div class="display-value">
            是否為偶數: {{ isEven ? '是' : '否' }}
          </div>
          <div class="display-value">
            格式化日期: {{ formattedCurrentDate }}
          </div>
        </div>
      </div>
    </div>

    <!-- 全域屬性與插件 -->
    <div class="demo-section">
      <h3>9. 全域屬性與插件使用</h3>
      <div class="comparison-grid">
        <div class="comparison-card vue2-card">
          <h4>Vue 2</h4>
          <div class="code-example">
            <pre v-pre><code>// main.js - 全域屬性
import Vue from 'vue'
import axios from 'axios'

Vue.prototype.$http = axios
Vue.prototype.$utils = {
  formatMoney: (amount) => `$${amount.toFixed(2)}`
}

// 使用插件
import VueRouter from 'vue-router'
Vue.use(VueRouter)

// 組件中使用
export default {
  async created() {
    // 使用全域屬性
    const response = await this.$http.get('/api/data')
    console.log(this.$utils.formatMoney(100))
  },
  methods: {
    async fetchData() {
      try {
        const result = await this.$http.get('/api/users')
        return result.data
      } catch (error) {
        console.error(error)
      }
    }
  }
}</code></pre>
          </div>
        </div>
        <div class="comparison-card vue3-card">
          <h4>Vue 3</h4>
          <div class="code-example">
            <pre v-pre><code>// main.js - 全域屬性
import { createApp } from 'vue'
import axios from 'axios'

const app = createApp(App)

app.config.globalProperties.$http = axios
app.config.globalProperties.$utils = {
  formatMoney: (amount) => `$${amount.toFixed(2)}`
}

// 使用插件
import { createRouter, createWebHistory } from 'vue-router'
const router = createRouter({
  history: createWebHistory(),
  routes: [...]
})
app.use(router)

// 組件中使用 - 方式1：getCurrentInstance (不推薦)
&lt;script setup&gt;
import { getCurrentInstance, onMounted } from 'vue'

const instance = getCurrentInstance()
const $http = instance?.appContext.config.globalProperties.$http
const $utils = instance?.appContext.config.globalProperties.$utils

onMounted(async () => {
  if ($http && $utils) {
    const response = await $http.get('/api/data')
    console.log($utils.formatMoney(100))
  }
})
&lt;/script&gt;

// 推薦方式2：使用 composables
&lt;script setup&gt;
import { useHttp } from '@/composables/useHttp'
import { useUtils } from '@/composables/useUtils'

const { get, post } = useHttp()
const { formatMoney } = useUtils()

const fetchData = async () => {
  const result = await get('/api/users')
  return result
}
&lt;/script&gt;</code></pre>
          </div>
        </div>
      </div>
    </div>

    <!-- 總結對比 -->
    <div class="demo-section">
      <h3>10. 主要差異總結</h3>
      <div class="comparison-grid">
        <div class="comparison-card vue2-card">
          <h4>Vue 2 特點</h4>
          <ul>
            <li>Options API：選項式 API</li>
            <li>this 上下文：通過 this 訪問數據</li>
            <li>data 函數：返回響應式對象</li>
            <li>組件選項：methods、computed、watch 等</li>
            <li>生命週期：beforeDestroy、destroyed</li>
            <li>混入：mixin 複用邏輯</li>
            <li>全域屬性：Vue.prototype 掛載</li>
            <li>工具函數：直接 import 使用</li>
          </ul>
        </div>
        <div class="comparison-card vue3-card">
          <h4>Vue 3 特點</h4>
          <ul>
            <li>Composition API：組合式 API</li>
            <li>setup 語法糖：更簡潔的寫法</li>
            <li>ref/reactive：明確的響應式聲明</li>
            <li>函數式：組合函數更好復用</li>
            <li>生命週期：onBeforeUnmount、onUnmounted</li>
            <li>組合函數：composables 複用邏輯</li>
            <li>全域屬性：app.config.globalProperties</li>
            <li>更好的 TypeScript 支援</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 響應式數據演示
const demoName = ref('')
const demoAge = ref(0)
const demoSkills = ref(['Vue.js'])

// 計算屬性演示
const firstName = ref('')
const lastName = ref('')

const fullName = computed(() => {
  return firstName.value + ' ' + lastName.value
})

// 事件處理演示
const demoCounter = ref(0)
const demoMessage = ref('')

// Composable 演示 - 模擬 useCounter
const composableCount = ref(0)
const isEven = computed(() => composableCount.value % 2 === 0)

// 模擬 useDate composable
const formattedCurrentDate = computed(() => {
  return new Date().toLocaleDateString('zh-TW')
})

// 方法
const addSkill = () => {
  const skills = ['JavaScript', 'TypeScript', 'CSS', 'HTML', 'Node.js', 'React']
  const randomSkill = skills[Math.floor(Math.random() * skills.length)]
  if (!demoSkills.value.includes(randomSkill)) {
    demoSkills.value.push(randomSkill)
  }
}

const increment = () => {
  demoCounter.value++
}

const handleDemoInput = (event) => {
  demoMessage.value = event.target.value
}

// Composable 方法
const composableIncrement = () => {
  composableCount.value++
}

const composableDecrement = () => {
  composableCount.value--
}

const composableReset = () => {
  composableCount.value = 0
}
</script>

<style scoped>
.vue2-vs-vue3-demo {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Arial', sans-serif;
}

.route-info {
  background: #f0f0f0;
  padding: 10px;
  border-radius: 5px;
  margin-bottom: 20px;
  font-family: monospace;
}

.demo-section {
  margin-bottom: 40px;
  border: 1px solid #e1e5e9;
  border-radius: 8px;
  padding: 20px;
  background: #fff;
}

.demo-section h3 {
  color: #2c3e50;
  margin-bottom: 20px;
  border-bottom: 2px solid #3498db;
  padding-bottom: 10px;
}

.comparison-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
  margin-bottom: 20px;
}

@media (max-width: 768px) {
  .comparison-grid {
    grid-template-columns: 1fr;
  }
}

.comparison-card {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 15px;
  background: #fafafa;
}

.vue2-card {
  border-left: 4px solid #e74c3c;
}

.vue2-card h4 {
  color: #e74c3c;
  margin-bottom: 15px;
}

.vue3-card {
  border-left: 4px solid #27ae60;
}

.vue3-card h4 {
  color: #27ae60;
  margin-bottom: 15px;
}

.code-example {
  background: #2d3748;
  border-radius: 6px;
  overflow-x: auto;
}

.code-example pre {
  margin: 0;
  padding: 15px;
  color: #e2e8f0;
  font-size: 13px;
  line-height: 1.5;
  font-family: 'Monaco', 'Menlo', 'Ubuntu Mono', monospace;
}

.demo-container {
  background: #f8f9fa;
  border: 1px solid #dee2e6;
  border-radius: 8px;
  padding: 20px;
  margin-top: 20px;
}

.demo-container h4 {
  color: #495057;
  margin-bottom: 15px;
}

.controls {
  display: flex;
  gap: 10px;
  margin-bottom: 15px;
  flex-wrap: wrap;
}

.input-field {
  padding: 8px 12px;
  border: 1px solid #ced4da;
  border-radius: 4px;
  font-size: 14px;
  flex: 1;
  min-width: 150px;
}

.btn {
  padding: 8px 16px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 14px;
  font-weight: 500;
  transition: background-color 0.2s;
}

.btn-primary {
  background: #007bff;
  color: white;
}

.btn-primary:hover {
  background: #0056b3;
}

.btn-secondary {
  background: #6c757d;
  color: white;
}

.btn-secondary:hover {
  background: #545b62;
}

.btn-danger {
  background: #dc3545;
  color: white;
}

.btn-danger:hover {
  background: #c82333;
}

.result {
  background: white;
  border: 1px solid #dee2e6;
  border-radius: 4px;
  padding: 15px;
}

.display-value {
  margin-bottom: 8px;
  padding: 8px;
  background: #e9ecef;
  border-radius: 4px;
  font-family: monospace;
}

.info-box {
  background: #d1ecf1;
  border: 1px solid #bee5eb;
  border-radius: 8px;
  padding: 20px;
  margin-top: 20px;
}

.info-box h4 {
  color: #0c5460;
  margin-bottom: 15px;
}

.info-box ul {
  margin: 0;
  padding-left: 20px;
}

.info-box li {
  margin-bottom: 8px;
  color: #0c5460;
}
</style>
