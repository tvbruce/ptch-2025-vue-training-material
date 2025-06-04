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

// 陣列類型
const skills = ref([])
// 或
const skills = reactive([])
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

// 立即執行
watch(() => user.name, (newVal) => {
  console.log('用戶名稱:', newVal)
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

    <!-- 總結對比 -->
    <div class="demo-section">
      <h3>7. 主要差異總結</h3>
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
</script>
