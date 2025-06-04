<template>
  <div class="props-demo">
    <h2>Props 屬性傳遞</h2>
    <p class="route-info">📍 路徑：/ComponentSamples/PropsDemo.vue</p>

    <!-- 基本 Props 用法 -->
    <div class="demo-section">
      <h3>1. 基本 Props 傳遞</h3>
      <div class="controls">
        <input v-model="userName" placeholder="輸入用戶名稱" class="input-field">
        <input v-model.number="userAge" type="number" placeholder="輸入年齡" class="input-field">
        <label class="checkbox-label">
          <input type="checkbox" v-model="isVip">
          VIP 用戶
        </label>
      </div>
      <div class="result">
        <UserCard :name="userName" :age="userAge" :is-vip="isVip" />
      </div>
      <div class="code-example">
        <pre v-pre><code><!-- 父組件 -->
&lt;UserCard :name="userName" :age="userAge" :is-vip="isVip" /&gt;

// 子組件 UserCard.vue
const props = defineProps({
  name: String,
  age: Number,
  isVip: Boolean
})

&lt;template&gt;
  &lt;div class="user-card"&gt;
    &lt;h4&gt;{{ props.name || '訪客' }}&lt;/h4&gt;
    &lt;p&gt;年齡: {{ props.age || '未提供' }}&lt;/p&gt;
    &lt;span v-if="props.isVip" class="vip-badge"&gt;VIP&lt;/span&gt;
  &lt;/div&gt;
&lt;/template&gt;</code></pre>
      </div>
    </div>

    <!-- Props 默認值 -->
    <div class="demo-section">
      <h3>2. Props 默認值與類型驗證</h3>
      <div class="controls">
        <input v-model="productName" placeholder="產品名稱" class="input-field">
        <input v-model.number="productPrice" type="number" placeholder="價格" class="input-field">
        <select v-model="productCategory" class="select-field">
          <option value="">選擇分類</option>
          <option value="electronics">電子產品</option>
          <option value="clothing">服飾</option>
          <option value="books">書籍</option>
        </select>
      </div>
      <div class="result">
        <ProductCard :name="productName" :price="productPrice" :category="productCategory" />
      </div>
      <div class="code-example">
        <pre v-pre><code>// ProductCard.vue - 帶默認值的 Props
const props = defineProps({
  name: {
    type: String,
    default: '未命名產品'
  },
  price: {
    type: Number,
    default: 0,
    validator: (value) => value >= 0
  },
  category: {
    type: String,
    default: 'general',
    validator: (value) =>
      ['electronics', 'clothing', 'books', 'general'].includes(value)
  }
})</code></pre>
      </div>
    </div>

    <!-- 複雜類型 Props -->
    <div class="demo-section">
      <h3>3. 複雜類型 Props (物件、陣列)</h3>
      <div class="controls">
        <button @click="addSkill" class="btn btn-primary">新增技能</button>
        <button @click="updateLocation" class="btn btn-secondary">更新位置</button>
      </div>
      <div class="result">
        <DeveloperProfile :profile="developerProfile" />
      </div>
      <div class="code-example">
        <pre v-pre><code>// DeveloperProfile.vue - 複雜類型 Props
const props = defineProps({
  profile: {
    type: Object,
    default: () => ({
      name: '開發者',
      skills: [],
      location: { city: '台北', country: '台灣' }
    }),
    validator: (value) => {
      return value && typeof value === 'object' &&
             Array.isArray(value.skills)
    }
  }
})

// 父組件傳遞
const developerProfile = ref({
  name: 'Vue 開發者',
  skills: ['JavaScript', 'Vue.js'],
  location: { city: '台北', country: '台灣' }
})</code></pre>
      </div>
    </div>

    <!-- Props 修改限制 -->
    <div class="demo-section">
      <h3>4. Props 的單向數據流</h3>
      <div class="info-box">
        <h4>重要概念：Props 是唯讀的</h4>
        <p>子組件不能直接修改 props，應該使用 emit 事件或 computed 屬性</p>
      </div>
      <div class="controls">
        <input v-model="initialCounter" type="number" placeholder="初始計數值" class="input-field">
      </div>
      <div class="result">
        <CounterWithProps :initial-value="initialCounter" @update:value="handleCounterUpdate" />
        <div class="display-value">
          父組件接收到的值: {{ counterValue }}
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// CounterWithProps.vue - 正確處理 Props 修改
const props = defineProps({
  initialValue: {
    type: Number,
    default: 0
  }
})

const emit = defineEmits(['update:value'])

// 使用本地狀態接收 props 值
const localValue = ref(props.initialValue)

// 當需要"修改"props時，發出事件
const increment = () => {
  localValue.value++
  emit('update:value', localValue.value)
}</code></pre>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue'
import UserCard from './components/UserCard.vue'
import ProductCard from './components/ProductCard.vue'
import DeveloperProfile from './components/DeveloperProfile.vue'
import CounterWithProps from './components/CounterWithProps.vue'

// 基本 Props 數據
const userName = ref('張三')
const userAge = ref(25)
const isVip = ref(false)

// 產品 Props 數據
const productName = ref('MacBook Pro')
const productPrice = ref(50000)
const productCategory = ref('electronics')

// 複雜類型 Props 數據
const developerProfile = reactive({
  name: 'Vue 開發者',
  skills: ['JavaScript', 'Vue.js', 'CSS'],
  location: { city: '台北', country: '台灣' }
})

// Props 修改相關
const initialCounter = ref(10)
const counterValue = ref(10)

// 方法
const addSkill = () => {
  const skills = ['TypeScript', 'Node.js', 'React', 'Angular', 'Python']
  const randomSkill = skills[Math.floor(Math.random() * skills.length)]
  if (!developerProfile.skills.includes(randomSkill)) {
    developerProfile.skills.push(randomSkill)
  }
}

const updateLocation = () => {
  const locations = [
    { city: '台中', country: '台灣' },
    { city: '高雄', country: '台灣' },
    { city: '新竹', country: '台灣' },
    { city: '台南', country: '台灣' }
  ]
  const randomLocation = locations[Math.floor(Math.random() * locations.length)]
  developerProfile.location = randomLocation
}

const handleCounterUpdate = (value) => {
  counterValue.value = value
}
</script>
