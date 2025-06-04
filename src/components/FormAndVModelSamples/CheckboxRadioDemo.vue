<!-- components/FormAndVModelSamples/CheckboxRadioDemo.vue -->
<template>
    <div class="checkbox-radio-demo">
        <h2>複選框與單選按鈕 (v-model)</h2>
        <p class="route-info">📍 路徑：/FormAndVModelSamples/CheckboxRadioDemo.vue</p>

        <!-- 單個複選框 -->
        <div class="demo-section">
            <h3>1. 單個複選框</h3>
            <div class="demo-grid">
                <div class="demo-item">
                    <div class="checkbox-group">
                        <label class="checkbox-label">
                            <input type="checkbox" v-model="singleCheckbox">
                            同意服務條款
                        </label>
                    </div>
                    <div class="output">
                        <div>值：{{ singleCheckbox }}</div>
                        <div>型別：{{ typeof singleCheckbox }}</div>
                        <div>狀態：{{ singleCheckbox ? '已勾選' : '未勾選' }}</div>
                    </div>
                </div>

                <div class="demo-item">
                    <div class="checkbox-group">
                        <label class="checkbox-label">
                            <input type="checkbox" v-model="enableNotifications">
                            接收通知
                        </label>
                        <label class="checkbox-label">
                            <input type="checkbox" v-model="enableUpdates" :disabled="!enableNotifications">
                            系統更新通知
                        </label>
                        <label class="checkbox-label">
                            <input type="checkbox" v-model="enablePromotions" :disabled="!enableNotifications">
                            促銷活動通知
                        </label>
                    </div>
                    <div class="output">
                        <div>通知設定狀態：</div>
                        <ul>
                            <li>接收通知：{{ enableNotifications ? '開啟' : '關閉' }}</li>
                            <li>系統更新：{{ enableUpdates ? '開啟' : '關閉' }}</li>
                            <li>促銷活動：{{ enablePromotions ? '開啟' : '關閉' }}</li>
                        </ul>
                    </div>
                </div>
            </div>

            <div class="code-example">
                <pre v-pre><code>&lt;!-- 單個複選框 --&gt;
&lt;input type="checkbox" v-model="singleCheckbox"&gt;

&lt;!-- 條件性啟用 --&gt;
&lt;input type="checkbox" v-model="enableNotifications"&gt;
&lt;input type="checkbox" v-model="enableUpdates" :disabled="!enableNotifications"&gt;

// 響應式數據 (布林值)
const singleCheckbox = ref(false)
const enableNotifications = ref(false)</code></pre>
            </div>
        </div>

        <!-- 多個複選框 -->
        <div class="demo-section">
            <h3>2. 多個複選框（陣列綁定）</h3>
            <div class="demo-grid">
                <div class="demo-item">
                    <div class="label">選擇你喜歡的程式語言：</div>
                    <div class="checkbox-group">
                        <label class="checkbox-label" v-for="lang in programmingLanguages" :key="lang">
                            <input type="checkbox" :value="lang" v-model="selectedLanguages">
                            {{ lang }}
                        </label>
                    </div>
                    <div class="output">
                        <div>已選擇：{{ selectedLanguages.length }} 項</div>
                        <div class="selected-items">
                            <span class="tag" v-for="lang in selectedLanguages" :key="lang">
                                {{ lang }}
                            </span>
                        </div>
                    </div>
                    <button class="action-btn" @click="selectAll"
                        :disabled="selectedLanguages.length === programmingLanguages.length">
                        全選
                    </button>
                    <button class="action-btn" @click="selectNone" :disabled="selectedLanguages.length === 0">
                        全部取消
                    </button>
                </div>

                <div class="demo-item">
                    <div class="label">選擇感興趣的主題：</div>
                    <div class="checkbox-group">
                        <label class="checkbox-label" v-for="topic in topics" :key="topic.id">
                            <input type="checkbox" :value="topic.id" v-model="selectedTopics">
                            {{ topic.name }}
                            <small>{{ topic.description }}</small>
                        </label>
                    </div>
                    <div class="output">
                        <div>選擇的主題 ID：{{ selectedTopics }}</div>
                        <div>選擇的主題名稱：</div>
                        <ul>
                            <li v-for="topicId in selectedTopics" :key="topicId">
                                {{ getTopicName(topicId) }}
                            </li>
                        </ul>
                    </div>
                </div>
            </div>

            <div class="code-example">
                <pre v-pre><code>&lt;!-- 多個複選框綁定到陣列 --&gt;
&lt;input type="checkbox" :value="lang" v-model="selectedLanguages"&gt;

// 響應式數據 (陣列)
const selectedLanguages = ref([])
const programmingLanguages = ['JavaScript', 'TypeScript', 'Python', 'Java', 'C#', 'Go', 'Rust', 'PHP']

// 當選中時，值會被加入陣列
// 當取消選中時，值會從陣列中移除</code></pre>
            </div>
        </div>

        <!-- 單選按鈕 -->
        <div class="demo-section">
            <h3>3. 單選按鈕</h3>
            <div class="demo-grid">
                <div class="demo-item">
                    <div class="label">選擇性別：</div>
                    <div class="radio-group">
                        <label class="radio-label">
                            <input type="radio" value="male" v-model="gender">
                            <span class="radio-text">男性</span>
                        </label>
                        <label class="radio-label">
                            <input type="radio" value="female" v-model="gender">
                            <span class="radio-text">女性</span>
                        </label>
                        <label class="radio-label">
                            <input type="radio" value="other" v-model="gender">
                            <span class="radio-text">其他</span>
                        </label>
                    </div>
                    <div class="output">
                        <div>選擇的性別：{{ gender || '未選擇' }}</div>
                        <div>型別：{{ typeof gender }}</div>
                    </div>
                </div>

                <div class="demo-item">
                    <div class="label">選擇等級：</div>
                    <div class="radio-group">
                        <label class="radio-label" v-for="level in levels" :key="level.value">
                            <input type="radio" :value="level.value" v-model="selectedLevel">
                            <span class="radio-text">
                                {{ level.name }}
                                <small>{{ level.description }}</small>
                            </span>
                        </label>
                    </div>
                    <div class="output">
                        <div>選擇的等級：{{ selectedLevel || '未選擇' }}</div>
                        <div class="level-info" v-if="selectedLevel">
                            <h5>等級資訊：</h5>
                            <p>{{ getLevelInfo(selectedLevel) }}</p>
                        </div>
                    </div>
                </div>
            </div>

            <div class="code-example">
                <pre v-pre><code>&lt;!-- 單選按鈕 --&gt;
&lt;input type="radio" value="male" v-model="gender"&gt;
&lt;input type="radio" value="female" v-model="gender"&gt;

// 響應式數據 (字串或其他值)
const gender = ref('')
const selectedLevel = ref('')

// 所有具有相同 v-model 的 radio button 形成一組
// 只能選擇其中一個值</code></pre>
            </div>
        </div>

        <!-- 進階用法 -->
        <div class="demo-section">
            <h3>4. 進階用法</h3>
            <div class="demo-grid">
                <div class="demo-item">
                    <div class="label">個人偏好設定：</div>
                    <div class="preference-group">
                        <label class="checkbox-label">
                            <input type="checkbox" v-model="preferences.newsletter">
                            訂閱電子報
                        </label>
                        <div v-if="preferences.newsletter" class="sub-options indent">
                            <label class="checkbox-label small">
                                <input type="checkbox" v-model="preferences.weeklyDigest">
                                週報摘要
                            </label>
                            <label class="checkbox-label small">
                                <input type="checkbox" v-model="preferences.dailyUpdates">
                                每日更新
                            </label>
                        </div>

                        <label class="checkbox-label">
                            <input type="checkbox" v-model="preferences.smsNotifications">
                            簡訊通知
                        </label>
                        <label class="checkbox-label">
                            <input type="checkbox" v-model="preferences.emailReminders">
                            郵件提醒
                        </label>
                    </div>

                    <div class="preference-summary">
                        <h5>偏好設定摘要：</h5>
                        <ul>
                            <li v-for="[key] in enabledPreferences" :key="key">
                                {{ formatPreferenceName(key) }}：已啟用
                            </li>
                        </ul>
                    </div>
                </div>
            </div>

            <div class="code-example">
                <pre v-pre><code>&lt;!-- 物件屬性綁定 --&gt;
&lt;input type="checkbox" v-model="preferences.newsletter"&gt;
&lt;input type="checkbox" v-model="preferences.smsNotifications"&gt;

// 響應式數據 (物件)
const preferences = ref({
  newsletter: false,
  weeklyDigest: false,
  dailyUpdates: false,
  smsNotifications: false,
  emailReminders: false
})</code></pre>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 單個複選框
const singleCheckbox = ref(false)
const enableNotifications = ref(false)
const enableUpdates = ref(false)
const enablePromotions = ref(false)

// 多個複選框
const selectedLanguages = ref([])
const programmingLanguages = ['JavaScript', 'TypeScript', 'Python', 'Java', 'C#', 'Go', 'Rust', 'PHP']

const selectedTopics = ref([])
const topics = [
    { id: 'frontend', name: '前端開發', description: 'HTML, CSS, JavaScript' },
    { id: 'backend', name: '後端開發', description: 'Server, Database, API' },
    { id: 'mobile', name: '行動開發', description: 'iOS, Android, React Native' },
    { id: 'devops', name: 'DevOps', description: 'CI/CD, Docker, Kubernetes' },
    { id: 'ai', name: '人工智慧', description: 'Machine Learning, Deep Learning' }
]

// 單選按鈕
const gender = ref('')
const selectedLevel = ref('')
const levels = [
    { value: 'beginner', name: '初學者', description: '剛開始學習程式設計' },
    { value: 'intermediate', name: '中級', description: '有一定基礎，能獨立開發' },
    { value: 'advanced', name: '高級', description: '經驗豐富，能解決複雜問題' },
    { value: 'expert', name: '專家', description: '領域專家，能指導他人' }
]

// 進階用法 - 物件綁定
const preferences = ref({
    newsletter: false,
    weeklyDigest: false,
    dailyUpdates: false,
    smsNotifications: false,
    emailReminders: false
})

// 方法
const selectAll = () => {
    selectedLanguages.value = [...programmingLanguages]
}

const selectNone = () => {
    selectedLanguages.value = []
}

const getTopicName = (topicId) => {
    const topic = topics.find(t => t.id === topicId)
    return topic ? topic.name : topicId
}

const getLevelInfo = (levelValue) => {
    const level = levels.find(l => l.value === levelValue)
    return level ? level.description : ''
}

const formatPreferenceName = (key) => {
    const names = {
        newsletter: '電子報',
        weeklyDigest: '週報摘要',
        dailyUpdates: '每日更新',
        smsNotifications: '簡訊通知',
        emailReminders: '郵件提醒'
    }
    return names[key] || key
}

// 計算屬性：過濾已啟用的偏好設定
const enabledPreferences = computed(() => {
    return Object.entries(preferences.value).filter(([key, value]) => value)
})
</script>
