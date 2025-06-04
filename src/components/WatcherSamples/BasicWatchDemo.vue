<!-- components/WatcherSamples/BasicWatchDemo.vue -->
<template>
    <div class="basic-watch-demo">
        <h2>基礎偵聽器用法</h2>
        <p class="route-info">📍 路徑：/WatcherSamples/BasicWatchDemo.vue</p>

        <!-- watch 基本用法 -->
        <div class="demo-section">
            <h3>1. watch 偵聽器</h3>
            <div class="description">
                watch 讓你明確指定要偵聽的數據源，當數據變化時執行回調函數。
            </div>
            <div class="controls">
                <input v-model="watchedValue" placeholder="輸入文字，觀察 watch 回調" class="input-field">
                <input v-model.number="watchedNumber" type="number" placeholder="輸入數字" class="input-field">
            </div>
            <div class="result">
                <div class="display-value">
                    <strong>當前值：</strong>{{ watchedValue }}
                </div>
                <div class="display-value">
                    <strong>當前數字：</strong>{{ watchedNumber }}
                </div>
                <div class="display-value">
                    <strong>watch 觸發次數：</strong>{{ watchCount }}
                </div>
                <div class="display-value">
                    <strong>最後變化：</strong>{{ lastWatchChange }}
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code>import { ref, watch } from 'vue'

const watchedValue = ref('')
const watchCount = ref(0)
const lastWatchChange = ref('')

// 偵聽單一數據源
watch(watchedValue, (newValue, oldValue) => {
  watchCount.value++
  lastWatchChange.value = `從 "${oldValue}" 變為 "${newValue}"`
})

// 偵聽多個數據源
watch([watchedValue, watchedNumber], ([newVal, newNum], [oldVal, oldNum]) => {
  console.log('多個值發生變化')
})</code></pre>
            </div>
        </div>

        <!-- watchEffect 基本用法 -->
        <div class="demo-section">
            <h3>2. watchEffect 偵聽器</h3>
            <div class="description">
                watchEffect 會自動追蹤回調函數中使用的響應式數據，無需明確指定數據源。
            </div>
            <div class="controls">
                <input v-model="effectValue1" placeholder="第一個值" class="input-field">
                <input v-model="effectValue2" placeholder="第二個值" class="input-field">
                <button @click="toggleEffectTracking" class="btn btn-primary">
                    {{ isEffectTracking ? '停止追蹤' : '開始追蹤' }}
                </button>
            </div>
            <div class="result">
                <div class="display-value">
                    <strong>計算結果：</strong>{{ computedFromEffect }}
                </div>
                <div class="display-value">
                    <strong>watchEffect 執行次數：</strong>{{ effectCount }}
                </div>
                <div class="display-value">
                    <strong>追蹤狀態：</strong>{{ isEffectTracking ? '正在追蹤' : '已停止' }}
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code>import { ref, watchEffect } from 'vue'

const effectValue1 = ref('')
const effectValue2 = ref('')
const effectCount = ref(0)

// watchEffect 自動追蹤依賴
const stop = watchEffect(() => {
  effectCount.value++
  // 這裡使用的任何響應式數據都會被自動追蹤
  computedFromEffect.value = `${effectValue1.value} + ${effectValue2.value}`
})

// 可以手動停止偵聽
const toggleEffectTracking = () => {
  if (isEffectTracking.value) {
    stop() // 停止偵聽
  } else {
    // 重新開始偵聽...
  }
}</code></pre>
            </div>
        </div>

        <!-- 立即執行對比 -->
        <div class="demo-section">
            <h3>3. 立即執行對比</h3>
            <div class="description">
                watch 預設惰性執行，watchEffect 立即執行。
            </div>
            <div class="controls">
                <input v-model="immediateValue" placeholder="測試立即執行" class="input-field">
                <button @click="resetCounts" class="btn btn-secondary">重置計數</button>
            </div>
            <div class="result">
                <div class="display-value">
                    <strong>當前值：</strong>{{ immediateValue }}
                </div>
                <div class="display-value info">
                    <strong>watch 執行次數：</strong>{{ watchImmediateCount }}
                    <small>（不包含初始執行）</small>
                </div>
                <div class="display-value info">
                    <strong>watchEffect 執行次數：</strong>{{ watchEffectImmediateCount }}
                    <small>（包含初始執行）</small>
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code>// watch: 惰性執行（不立即執行）
watch(immediateValue, () => {
  watchImmediateCount.value++
})

// watch with immediate: 立即執行
watch(immediateValue, () => {
  // 立即執行一次，然後每次變化都執行
}, { immediate: true })

// watchEffect: 總是立即執行
watchEffect(() => {
  watchEffectImmediateCount.value++
  // 即使 immediateValue 沒有變化，這個函數也會立即執行一次
  console.log('watchEffect 執行', immediateValue.value)
})</code></pre>
            </div>
        </div>

        <!-- 深度偵聽 -->
        <div class="demo-section">
            <h3>4. 深度偵聽</h3>
            <div class="description">
                偵聽物件內部屬性的變化。
            </div>
            <div class="controls">
                <input v-model="deepObject.name" placeholder="姓名" class="input-field">
                <input v-model.number="deepObject.age" type="number" placeholder="年齡" class="input-field">
                <input v-model="deepObject.info.email" placeholder="電子郵件" class="input-field">
                <button @click="resetDeepObject" class="btn btn-warning">重置物件</button>
            </div>
            <div class="result">
                <div class="display-value">
                    <strong>物件內容：</strong>
                    <pre class="object-display">{{ JSON.stringify(deepObject, null, 2) }}</pre>
                </div>
                <div class="display-value">
                    <strong>深度 watch 觸發次數：</strong>{{ deepWatchCount }}
                </div>
                <div class="display-value">
                    <strong>屬性 watch 觸發次數：</strong>{{ propertyWatchCount }}
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code>const deepObject = ref({
  name: '',
  age: 0,
  info: { email: '' }
})

// 深度偵聽整個物件
watch(deepObject, (newValue, oldValue) => {
  deepWatchCount.value++
}, { deep: true })

// 偵聽特定屬性
watch(() => deepObject.value.name, (newName, oldName) => {
  propertyWatchCount.value++
  console.log(`姓名從 ${oldName} 變為 ${newName}`)
})

// watchEffect 自動深度追蹤
watchEffect(() => {
  // 會追蹤 deepObject 內所有使用到的屬性
  if (deepObject.value.name && deepObject.value.age) {
    console.log('有效用戶:', deepObject.value)
  }
})</code></pre>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, watch, watchEffect } from 'vue'

// watch 基本用法
const watchedValue = ref('')
const watchedNumber = ref(0)
const watchCount = ref(0)
const lastWatchChange = ref('尚未發生變化')

watch(watchedValue, (newValue, oldValue) => {
    watchCount.value++
    lastWatchChange.value = `從 "${oldValue}" 變為 "${newValue}"`
})

watch([watchedValue, watchedNumber], () => {
    console.log('多個值發生變化')
})

// watchEffect 基本用法
const effectValue1 = ref('')
const effectValue2 = ref('')
const effectCount = ref(0)
const computedFromEffect = ref('')
const isEffectTracking = ref(true)

let stopEffect = watchEffect(() => {
    if (isEffectTracking.value) {
        effectCount.value++
        computedFromEffect.value = `${effectValue1.value} + ${effectValue2.value}`
    }
})

const toggleEffectTracking = () => {
    if (isEffectTracking.value) {
        stopEffect()
        isEffectTracking.value = false
    } else {
        isEffectTracking.value = true
        stopEffect = watchEffect(() => {
            if (isEffectTracking.value) {
                effectCount.value++
                computedFromEffect.value = `${effectValue1.value} + ${effectValue2.value}`
            }
        })
    }
}

// 立即執行對比
const immediateValue = ref('')
const watchImmediateCount = ref(0)
const watchEffectImmediateCount = ref(0)

watch(immediateValue, () => {
    watchImmediateCount.value++
})

watchEffect(() => {
    watchEffectImmediateCount.value++
    // 讀取 immediateValue 以建立依賴
    console.log('watchEffect 執行:', immediateValue.value)
})

const resetCounts = () => {
    watchImmediateCount.value = 0
    watchEffectImmediateCount.value = 0
}

// 深度偵聽
const deepObject = ref({
    name: '',
    age: 0,
    info: {
        email: ''
    }
})

const deepWatchCount = ref(0)
const propertyWatchCount = ref(0)

watch(deepObject, () => {
    deepWatchCount.value++
}, { deep: true })

watch(() => deepObject.value.name, (newName, oldName) => {
    propertyWatchCount.value++
    console.log(`姓名從 ${oldName} 變為 ${newName}`)
})

watchEffect(() => {
    if (deepObject.value.name && deepObject.value.age) {
        console.log('有效用戶:', deepObject.value)
    }
})

const resetDeepObject = () => {
    deepObject.value = {
        name: '',
        age: 0,
        info: {
            email: ''
        }
    }
}
</script>
