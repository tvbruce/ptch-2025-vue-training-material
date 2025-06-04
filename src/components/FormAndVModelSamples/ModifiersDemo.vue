<!-- components/FormAndVModelSamples/ModifiersDemo.vue -->
<template>
    <div class="modifiers-demo">
        <h2>v-model 修飾符</h2>
        <p class="route-info">📍 路徑：/FormAndVModelSamples/ModifiersDemo.vue</p>

        <!-- .lazy 修飾符 -->
        <div class="demo-section">
            <h3>1. .lazy 修飾符</h3>
            <p class="description">預設情況下，v-model 在每次 input 事件後同步數據。加上 .lazy 修飾符後，會改為在 change 事件後同步。</p>

            <div class="demo-grid">
                <div class="demo-item">
                    <label>預設行為 (即時同步)：</label>
                    <input type="text" v-model="normalInput" placeholder="輸入文字試試">
                    <div class="output">即時值：{{ normalInput }}</div>
                    <div class="update-count">更新次數：{{ normalUpdateCount }}</div>
                </div>

                <div class="demo-item">
                    <label>使用 .lazy (失去焦點時同步)：</label>
                    <input type="text" v-model.lazy="lazyInput" placeholder="輸入文字然後失去焦點">
                    <div class="output">同步值：{{ lazyInput }}</div>
                    <div class="update-count">更新次數：{{ lazyUpdateCount }}</div>
                </div>
            </div>

            <div class="input-comparison">
                <div class="calculation">
                    <strong>效能差異：</strong>
                    即時更新了 {{ normalUpdateCount }} 次，延遲更新了 {{ lazyUpdateCount }} 次
                    <span v-if="normalUpdateCount > lazyUpdateCount">
                        (節省了 {{ normalUpdateCount - lazyUpdateCount }} 次更新)
                    </span>
                </div>
            </div>

            <div class="code-example">
                <pre v-pre><code>&lt;!-- 預設行為：每次輸入都觸發 --&gt;
&lt;input v-model="normalInput"&gt;

&lt;!-- .lazy 修飾符：失去焦點或按 Enter 時才觸發 --&gt;
&lt;input v-model.lazy="lazyInput"&gt;

// 適用場景：
// - 大型表單減少不必要的驗證
// - 複雜計算的輸入框
// - 即時搜索的延遲處理</code></pre>
            </div>
        </div>

        <!-- .number 修飾符 -->
        <div class="demo-section">
            <h3>2. .number 修飾符</h3>
            <p class="description">自動將輸入值轉換為數字類型。如果輸入的值無法被 parseFloat() 解析，則會返回原始的值。</p>

            <div class="demo-grid">
                <div class="demo-item">
                    <label>不使用 .number：</label>
                    <input type="text" v-model="stringNumber" placeholder="輸入數字">
                    <div class="output">
                        <div>值：{{ stringNumber }}</div>
                        <div>型別：{{ typeof stringNumber }}</div>
                        <div class="type-badge">{{ typeof stringNumber }}</div>
                    </div>
                </div>

                <div class="demo-item">
                    <label>使用 .number：</label>
                    <input type="text" v-model.number="realNumber" placeholder="輸入數字">
                    <div class="output">
                        <div>值：{{ realNumber }}</div>
                        <div>型別：{{ typeof realNumber }}</div>
                        <div class="type-badge">{{ typeof realNumber }}</div>
                    </div>
                </div>
            </div>

            <div class="number-operations">
                <h4>數學運算示例：</h4>
                <div class="calc-grid">
                    <div class="calc-item">
                        <label>數字A (.number)：</label>
                        <input type="text" v-model.number="numberA" placeholder="輸入數字">
                        <div class="result">值：{{ numberA }} ({{ typeof numberA }})</div>
                    </div>
                    <div class="calc-item">
                        <label>數字B (.number)：</label>
                        <input type="text" v-model.number="numberB" placeholder="輸入數字">
                        <div class="result">值：{{ numberB }} ({{ typeof numberB }})</div>
                    </div>
                </div>
                <p><strong>加法結果：</strong> {{ calculationResult }}</p>
                <p><strong>說明：</strong> {{ calculationExplanation }}</p>
            </div>

            <div class="code-example">
                <pre v-pre><code>&lt;!-- 字串型別 --&gt;
&lt;input v-model="stringNumber"&gt;
// stringNumber 的值是 "123" (字串)

&lt;!-- 數字型別 --&gt;
&lt;input v-model.number="realNumber"&gt;
// realNumber 的值是 123 (數字)

// 數學運算
"5" + "3" = "53" (字串拼接)
5 + 3 = 8 (數學加法)</code></pre>
            </div>
        </div>

        <!-- .trim 修飾符 -->
        <div class="demo-section">
            <h3>3. .trim 修飾符</h3>
            <p class="description">自動過濾用戶輸入的首尾空白字符。</p>

            <div class="demo-grid">
                <div class="demo-item">
                    <label>不使用 .trim：</label>
                    <input type="text" v-model="untrimmedText" placeholder="輸入前後帶空格的文字">
                    <div class="output">
                        <div>長度：{{ untrimmedText.length }} 字元</div>
                        <div class="whitespace-visual">"<span>{{ untrimmedText }}</span>"</div>
                    </div>
                </div>

                <div class="demo-item">
                    <label>使用 .trim：</label>
                    <input type="text" v-model.trim="trimmedText" placeholder="輸入前後帶空格的文字">
                    <div class="output">
                        <div>長度：{{ trimmedText.length }} 字元</div>
                        <div class="whitespace-visual">"<span>{{ trimmedText }}</span>"</div>
                    </div>
                </div>
            </div>

            <div class="trim-examples">
                <h4>常見應用場景：</h4>
                <div class="scenario-grid">
                    <div class="scenario">
                        <label>用戶名稱：</label>
                        <input type="text" v-model.trim="username" placeholder="請輸入用戶名">
                        <div class="validation"
                            :class="{ valid: isValidUsername, invalid: username && !isValidUsername }">
                            {{ username ? (isValidUsername ? '✅ 有效的用戶名' : '❌ 用戶名不能包含空格') : '請輸入用戶名' }}
                        </div>
                    </div>

                    <div class="scenario">
                        <label>郵件地址：</label>
                        <input type="email" v-model.trim="email" placeholder="請輸入郵件地址">
                        <div class="validation" :class="{ valid: isValidEmail, invalid: email && !isValidEmail }">
                            {{ email ? (isValidEmail ? '✅ 有效的郵件格式' : '❌ 郵件格式不正確') : '請輸入郵件地址' }}
                        </div>
                    </div>
                </div>
            </div>

            <div class="code-example">
                <pre v-pre><code>&lt;!-- 不使用 .trim --&gt;
&lt;input v-model="untrimmedText"&gt;
// 輸入 "  hello  " 得到 "  hello  "

&lt;!-- 使用 .trim --&gt;
&lt;input v-model.trim="trimmedText"&gt;
// 輸入 "  hello  " 得到 "hello"

// 常用於：用戶名、密碼、郵件地址等不應該有首尾空格的輸入</code></pre>
            </div>
        </div>

        <!-- 組合使用修飾符 -->
        <div class="demo-section">
            <h3>4. 組合使用修飾符</h3>
            <p class="description">多個修飾符可以一起使用，處理順序為：trim → number → lazy。</p>

            <div class="combined-examples">
                <div class="example-group">
                    <h5>.trim.number 組合：</h5>
                    <input type="text" v-model.trim.number="trimmedNumber" placeholder="輸入帶空格的數字">
                    <div class="output">
                        <div>值：{{ trimmedNumber }}</div>
                        <div>型別：{{ typeof trimmedNumber }}</div>
                    </div>
                </div>

                <div class="example-group">
                    <h5>.lazy.trim.number 組合：</h5>
                    <input type="text" v-model.lazy.trim.number="lazyTrimmedNumber" placeholder="失去焦點時處理">
                    <div class="output">
                        <div>值：{{ lazyTrimmedNumber }}</div>
                        <div>型別：{{ typeof lazyTrimmedNumber }}</div>
                    </div>
                </div>
            </div>

            <div class="processing-steps">
                <h4>處理步驟示例：</h4>
                <div class="step">
                    <span class="step-label">1. 用戶輸入：</span> " 123.45 "
                </div>
                <div class="step">
                    <span class="step-label">2. .trim 處理：</span> "123.45"
                </div>
                <div class="step">
                    <span class="step-label">3. .number 處理：</span> 123.45
                </div>
                <div class="step">
                    <span class="step-label">4. 最終結果：</span> 123.45 (number 類型)
                </div>
            </div>

            <div class="code-example">
                <pre v-pre><code>&lt;!-- 組合使用修飾符 --&gt;
&lt;input v-model.trim.number="trimmedNumber"&gt;
&lt;input v-model.lazy.trim.number="lazyTrimmedNumber"&gt;

// 處理順序：
// 1. .trim - 移除首尾空格
// 2. .number - 轉換為數字
// 3. .lazy - 延遲觸發 (如果有的話)</code></pre>
            </div>
        </div>

        <!-- 效能測試 -->
        <div class="demo-section">
            <h3>5. 效能測試與最佳實踐</h3>
            <div class="performance-test">
                <h4>渲染次數測試：</h4>
                <div class="test-inputs">
                    <div class="test-group">
                        <label>一般輸入框：</label>
                        <input type="text" v-model="performanceTest.normal" placeholder="輸入文字">
                        <div class="render-count">渲染次數：{{ performanceTest.normalRenderCount }}</div>
                    </div>

                    <div class="test-group">
                        <label>使用 .lazy：</label>
                        <input type="text" v-model.lazy="performanceTest.lazy" placeholder="輸入文字">
                        <div class="render-count">渲染次數：{{ performanceTest.lazyRenderCount }}</div>
                    </div>
                </div>
            </div>

            <div class="best-practices">
                <h4>最佳實踐建議：</h4>
                <div class="practice-grid">
                    <div class="practice-item good">
                        <h6>✅ 建議使用</h6>
                        <ul>
                            <li>表單驗證使用 .lazy 減少不必要的檢查</li>
                            <li>數字計算使用 .number 確保類型正確</li>
                            <li>用戶資料輸入使用 .trim 清理空格</li>
                            <li>組合使用修飾符提高數據品質</li>
                        </ul>
                    </div>

                    <div class="practice-item caution">
                        <h6>⚠️ 注意事項</h6>
                        <ul>
                            <li>.number 無法解析時會回傳原始值</li>
                            <li>修飾符順序會影響處理結果</li>
                            <li>.lazy 可能影響使用者體驗</li>
                            <li>過度使用修飾符可能增加複雜度</li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, watch } from 'vue'

// .lazy 修飾符
const normalInput = ref('')
const lazyInput = ref('')
const normalUpdateCount = ref(0)
const lazyUpdateCount = ref(0)

// .number 修飾符
const stringNumber = ref('')
const realNumber = ref('')
const numberA = ref('')
const numberB = ref('')

// .trim 修飾符
const untrimmedText = ref('')
const trimmedText = ref('')
const username = ref('')
const email = ref('')

// 組合修飾符
const trimmedNumber = ref('')
const lazyTrimmedNumber = ref('')

// 效能測試
const performanceTest = ref({
    normal: '',
    lazy: '',
    normalRenderCount: 0,
    lazyRenderCount: 0
})

// 監聽器計算更新次數
watch(normalInput, () => {
    normalUpdateCount.value++
}, { immediate: false })

watch(lazyInput, () => {
    lazyUpdateCount.value++
}, { immediate: false })

watch(() => performanceTest.value.normal, () => {
    performanceTest.value.normalRenderCount++
}, { immediate: false })

watch(() => performanceTest.value.lazy, () => {
    performanceTest.value.lazyRenderCount++
}, { immediate: false })

// 計算屬性
const calculationResult = computed(() => {
    if (typeof numberA.value === 'number' && typeof numberB.value === 'number') {
        return numberA.value + numberB.value
    }
    return `${numberA.value}${numberB.value}`
})

const calculationExplanation = computed(() => {
    if (typeof numberA.value === 'number' && typeof numberB.value === 'number') {
        return '數字相加 (數學運算)'
    }
    return '字串拼接'
})

const isValidUsername = computed(() => {
    return username.value && !/\s/.test(username.value) && username.value.length >= 3
})

const isValidEmail = computed(() => {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
    return email.value && emailRegex.test(email.value)
})
</script>
