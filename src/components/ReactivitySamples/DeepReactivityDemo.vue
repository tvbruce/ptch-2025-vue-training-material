<!-- components/ReactivitySamples/DeepReactivityDemo.vue -->
<template>
  <div class="deep-reactivity-demo">
    <h2>深層響應性展示</h2>
    <p class="route-info">📍 路徑：/ReactivitySamples/DeepReactivityDemo.vue</p>

    <!-- ref 深層響應 -->
    <div class="demo-section">
      <h3>1. ref 的深層響應</h3>
      <div class="controls">
        <input v-model="refData.user.profile.name" placeholder="姓名" class="input-field">
        <input v-model="refData.user.profile.bio" placeholder="簡介" class="input-field">
        <button @click="addRefHobby" class="btn btn-primary">新增興趣</button>
        <button @click="resetRefData" class="btn btn-secondary">重置</button>
      </div>
      <div class="result">
        <div class="display-value">姓名: {{ refData.user.profile.name }}</div>
        <div class="display-value">簡介: {{ refData.user.profile.bio }}</div>
        <div class="display-value">興趣: {{ refData.user.hobbies.join(', ') }}</div>
        <div class="display-value">更新次數: {{ refUpdateCount }}</div>
      </div>
      <div class="code-example">
        <pre v-pre><code>const refData = ref({
  user: {
    profile: { name: '', bio: '' },
    hobbies: []
  }
})

// 深層屬性也是響應式的
refData.value.user.profile.name = '新名字'
refData.value.user.hobbies.push('閱讀')</code></pre>
      </div>
    </div>

    <!-- reactive 深層響應 -->
    <div class="demo-section">
      <h3>2. reactive 的深層響應</h3>
      <div class="controls">
        <input v-model="reactiveData.company.info.name" placeholder="公司名稱" class="input-field">
        <input v-model="reactiveData.company.info.address" placeholder="地址" class="input-field">
        <button @click="addEmployee" class="btn btn-success">新增員工</button>
        <button @click="resetReactiveData" class="btn btn-secondary">重置</button>
      </div>
      <div class="result">
        <div class="display-value">公司: {{ reactiveData.company.info.name }}</div>
        <div class="display-value">地址: {{ reactiveData.company.info.address }}</div>
        <div class="display-value">員工數: {{ reactiveData.company.employees.length }}</div>
        <div class="display-value">更新次數: {{ reactiveUpdateCount }}</div>
      </div>
      <div class="employee-list">
        <div v-for="(employee, index) in reactiveData.company.employees" :key="index" class="employee-item">
          <input v-model="employee.name" placeholder="員工姓名" class="input-field small">
          <input v-model="employee.position" placeholder="職位" class="input-field small">
          <button @click="removeEmployee(index)" class="btn-small">刪除</button>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>const reactiveData = reactive({
  company: {
    info: { name: '', address: '' },
    employees: []
  }
})

// 深層屬性也是響應式的
reactiveData.company.info.name = '新公司'
reactiveData.company.employees.push({ name: '張三', position: '工程師' })</code></pre>
      </div>
    </div>

    <!-- shallowRef vs ref -->
    <div class="demo-section">
      <h3>3. shallowRef vs ref 對比</h3>
      <div class="comparison-grid">
        <div class="comparison-item">
          <h4>shallowRef (淺層響應)</h4>
          <div class="controls">
            <button @click="changeShallowRefProperty" class="btn btn-warning">
              修改屬性 (不響應)
            </button>
            <button @click="replaceShallowRefObject" class="btn btn-primary">
              替換物件 (響應)
            </button>
          </div>
          <div class="result">
            <div class="display-value">名稱: {{ shallowRefData.name }}</div>
            <div class="display-value">計數: {{ shallowRefData.count }}</div>
            <div class="display-value">更新次數: {{ shallowUpdateCount }}</div>
          </div>
          <div class="code-example">
            <pre v-pre><code>const shallowRefData = shallowRef({
  name: 'test',
  count: 0
})

// ❌ 不會觸發響應
shallowRefData.value.count++

// ✅ 會觸發響應
shallowRefData.value = { ...shallowRefData.value }</code></pre>
          </div>
        </div>

        <div class="comparison-item">
          <h4>ref (深層響應)</h4>
          <div class="controls">
            <button @click="changeDeepRefProperty" class="btn btn-success">
              修改屬性 (響應)
            </button>
            <button @click="replaceDeepRefObject" class="btn btn-primary">
              替換物件 (響應)
            </button>
          </div>
          <div class="result">
            <div class="display-value">名稱: {{ deepRefData.name }}</div>
            <div class="display-value">計數: {{ deepRefData.count }}</div>
            <div class="display-value">更新次數: {{ deepUpdateCount }}</div>
          </div>
          <div class="code-example">
            <pre v-pre><code>const deepRefData = ref({
  name: 'test',
  count: 0
})

// ✅ 會觸發響應
deepRefData.value.count++

// ✅ 會觸發響應
deepRefData.value = { ...deepRefData.value }</code></pre>
          </div>
        </div>
      </div>
    </div>

    <!-- 性能考量 -->
    <div class="demo-section">
      <h3>4. 性能考量</h3>
      <div class="performance-info">
        <div class="info-card">
          <h4>💡 深層響應的代價</h4>
          <ul>
            <li>Vue 會遞歸地將物件的所有屬性轉換為響應式</li>
            <li>對於大型物件或深層嵌套，可能影響性能</li>
            <li>如果不需要深層響應，可以考慮使用 shallowRef 或 shallowReactive</li>
          </ul>
        </div>
        <div class="info-card">
          <h4>🚀 優化建議</h4>
          <ul>
            <li>只對需要響應的數據使用響應式 API</li>
            <li>大型靜態數據可以使用 markRaw() 標記</li>
            <li>考慮數據結構的扁平化</li>
            <li>使用 shallowRef 處理大型列表</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, shallowRef, watch } from 'vue'

// ref 深層響應
const refData = ref({
  user: {
    profile: {
      name: '',
      bio: ''
    },
    hobbies: []
  }
})

const refUpdateCount = ref(0)

// reactive 深層響應
const reactiveData = reactive({
  company: {
    info: {
      name: '',
      address: ''
    },
    employees: []
  }
})

const reactiveUpdateCount = ref(0)

// shallowRef vs ref
const shallowRefData = shallowRef({
  name: 'test',
  count: 0
})

const deepRefData = ref({
  name: 'test',
  count: 0
})

const shallowUpdateCount = ref(0)
const deepUpdateCount = ref(0)

// 監聽更新次數
watch(refData, () => {
  refUpdateCount.value++
}, { deep: true })

watch(reactiveData, () => {
  reactiveUpdateCount.value++
}, { deep: true })

watch(shallowRefData, () => {
  shallowUpdateCount.value++
})

watch(deepRefData, () => {
  deepUpdateCount.value++
}, { deep: true })

// 方法
const addRefHobby = () => {
  const hobbies = ['閱讀', '游泳', '攝影', '旅行', '音樂', '烹飪']
  const randomHobby = hobbies[Math.floor(Math.random() * hobbies.length)]
  if (!refData.value.user.hobbies.includes(randomHobby)) {
    refData.value.user.hobbies.push(randomHobby)
  }
}

const resetRefData = () => {
  refData.value = {
    user: {
      profile: { name: '', bio: '' },
      hobbies: []
    }
  }
}

const addEmployee = () => {
  reactiveData.company.employees.push({
    name: '',
    position: ''
  })
}

const removeEmployee = (index) => {
  reactiveData.company.employees.splice(index, 1)
}

const resetReactiveData = () => {
  reactiveData.company.info.name = ''
  reactiveData.company.info.address = ''
  reactiveData.company.employees.splice(0)
}

const changeShallowRefProperty = () => {
  // 這不會觸發響應式更新
  shallowRefData.value.count++
  shallowRefData.value.name = `test-${Date.now()}`
}

const replaceShallowRefObject = () => {
  // 這會觸發響應式更新
  shallowRefData.value = {
    ...shallowRefData.value,
    count: shallowRefData.value.count + 1
  }
}

const changeDeepRefProperty = () => {
  // 這會觸發響應式更新
  deepRefData.value.count++
  deepRefData.value.name = `test-${Date.now()}`
}

const replaceDeepRefObject = () => {
  // 這也會觸發響應式更新
  deepRefData.value = {
    ...deepRefData.value,
    count: deepRefData.value.count + 1
  }
}
</script>
