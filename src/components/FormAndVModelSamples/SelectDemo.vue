<!-- components/FormAndVModelSamples/SelectDemo.vue -->
<template>
    <div class="select-demo">
        <h2>下拉選擇框 (v-model)</h2>
        <p class="route-info">📍 路徑：/FormAndVModelSamples/SelectDemo.vue</p>

        <!-- 單選下拉框 -->
        <div class="demo-section">
            <h3>1. 單選下拉框</h3>
            <div class="demo-grid">
                <div class="demo-item">
                    <label>選擇城市：</label>
                    <select v-model="selectedCity">
                        <option value="" disabled>請選擇城市</option>
                        <option v-for="city in cities" :key="city.id" :value="city.id">
                            {{ city.name }}
                        </option>
                    </select>
                    <div class="output">
                        <div>選擇的城市 ID：{{ selectedCity || '未選擇' }}</div>
                        <div class="city-info" v-if="selectedCity">
                            <h5>城市資訊：</h5>
                            <p>名稱：{{ getCityInfo(selectedCity)?.name }}</p>
                            <p>地區：<span class="region-tag">{{ getCityInfo(selectedCity)?.region }}</span></p>
                            <p>人口：{{ getCityInfo(selectedCity)?.population?.toLocaleString() }} 人</p>
                        </div>
                    </div>
                </div>

                <div class="demo-item">
                    <label>選擇國家：</label>
                    <select v-model="selectedCountry">
                        <option value="">所有國家</option>
                        <option value="tw">台灣</option>
                        <option value="jp">日本</option>
                        <option value="kr">韓國</option>
                        <option value="us">美國</option>
                        <option value="cn">中國</option>
                    </select>
                    <div class="output">
                        <div>選擇的國家：{{ selectedCountry || '所有國家' }}</div>
                        <div>資料型別：{{ typeof selectedCountry }}</div>
                        <div>是否為空字串：{{ selectedCountry === '' ? '是' : '否' }}</div>
                    </div>
                </div>
            </div>

            <div class="code-example">
                <pre v-pre><code>&lt;!-- 單選下拉框 --&gt;
&lt;select v-model="selectedCity"&gt;
  &lt;option value="" disabled&gt;請選擇城市&lt;/option&gt;
  &lt;option v-for="city in cities" :key="city.id" :value="city.id"&gt;
    {{ city.name }}
  &lt;/option&gt;
&lt;/select&gt;

// 響應式數據
const selectedCity = ref('')
const cities = [
  { id: 'taipei', name: '台北', region: '北部', population: 2600000 },
  { id: 'taichung', name: '台中', region: '中部', population: 2800000 }
]</code></pre>
            </div>
        </div>

        <!-- 多選下拉框 -->
        <div class="demo-section">
            <h3>2. 多選下拉框</h3>
            <div class="demo-grid">
                <div class="demo-item">
                    <label>選擇程式語言 (按住 Ctrl/Cmd 多選)：</label>
                    <select v-model="selectedLanguages" multiple>
                        <option v-for="lang in programmingLanguages" :key="lang.id" :value="lang.id">
                            {{ lang.name }} - {{ lang.type }}
                        </option>
                    </select>
                    <div class="output">
                        <div>已選擇：{{ selectedLanguages.length }} 項</div>
                        <div class="selected-languages">
                            <span class="language-tag" v-for="langId in selectedLanguages" :key="langId">
                                {{ getLanguageName(langId) }}
                            </span>
                        </div>
                        <div class="language-stats" v-if="selectedLanguages.length > 0">
                            <h5>統計資訊：</h5>
                            <div class="stats-grid">
                                <div class="stat-item">
                                    <span class="stat-label">前端：</span>
                                    <span class="stat-value">{{ countLanguagesByType('frontend') }}</span>
                                </div>
                                <div class="stat-item">
                                    <span class="stat-label">後端：</span>
                                    <span class="stat-value">{{ countLanguagesByType('backend') }}</span>
                                </div>
                                <div class="stat-item">
                                    <span class="stat-label">通用：</span>
                                    <span class="stat-value">{{ countLanguagesByType('general') }}</span>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <div class="code-example">
                <pre v-pre><code>&lt;!-- 多選下拉框 --&gt;
&lt;select v-model="selectedLanguages" multiple&gt;
  &lt;option v-for="lang in programmingLanguages" :key="lang.id" :value="lang.id"&gt;
    {{ lang.name }}
  &lt;/option&gt;
&lt;/select&gt;

// 響應式數據 (陣列)
const selectedLanguages = ref([])
const programmingLanguages = [
  { id: 'js', name: 'JavaScript', type: 'frontend' },
  { id: 'py', name: 'Python', type: 'backend' }
]</code></pre>
            </div>
        </div>

        <!-- 動態選項 -->
        <div class="demo-section">
            <h3>3. 動態選項與串接</h3>
            <div class="demo-grid">
                <div class="demo-item">
                    <div class="cascading-selects">
                        <div class="select-group">
                            <label>職業類別：</label>
                            <select v-model="selectedCategory">
                                <option value="" disabled>請選擇類別</option>
                                <option v-for="category in jobCategories" :key="category.id" :value="category.id">
                                    {{ category.name }}
                                </option>
                            </select>
                        </div>

                        <div class="select-group">
                            <label>具體職業：</label>
                            <select v-model="selectedJob" :disabled="!selectedCategory">
                                <option value="" disabled>請先選擇類別</option>
                                <option v-for="job in availableJobs" :key="job.id" :value="job.id">
                                    {{ job.title }}
                                </option>
                            </select>
                        </div>

                        <div class="select-group">
                            <label>技能要求：</label>
                            <select v-model="selectedSkills" multiple :disabled="!selectedJob">
                                <option v-for="skill in requiredSkills" :key="skill" :value="skill">
                                    {{ skill }}
                                </option>
                            </select>
                        </div>
                    </div>

                    <div class="output" v-if="selectedJob">
                        <div class="location-summary">
                            <h5>選擇摘要：</h5>
                            <div class="breadcrumb">
                                {{ getCategoryName(selectedCategory) }} > {{ getJobTitle(selectedJob) }}
                            </div>
                            <div class="career-tags">
                                <span class="skill-tag" v-for="skill in selectedSkills" :key="skill">
                                    {{ skill }}
                                </span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <div class="code-example">
                <pre v-pre><code>&lt;!-- 串接式下拉框 --&gt;
&lt;select v-model="selectedCategory"&gt;
  &lt;option v-for="category in jobCategories" :value="category.id"&gt;
    {{ category.name }}
  &lt;/option&gt;
&lt;/select&gt;

&lt;select v-model="selectedJob" :disabled="!selectedCategory"&gt;
  &lt;option v-for="job in availableJobs" :value="job.id"&gt;
    {{ job.title }}
  &lt;/option&gt;
&lt;/select&gt;

// 計算屬性：根據類別過濾職業
const availableJobs = computed(() => {
  if (!selectedCategory.value) return []
  return jobs.filter(job => job.categoryId === selectedCategory.value)
})</code></pre>
            </div>
        </div>

        <!-- 自訂樣式選項 -->
        <div class="demo-section">
            <h3>4. 自訂樣式與主題</h3>
            <div class="demo-grid">
                <div class="demo-item">
                    <div class="custom-select-wrapper">
                        <label>選擇主題：</label>
                        <select v-model="selectedTheme" class="custom-select">
                            <option value="light">淺色主題</option>
                            <option value="dark">深色主題</option>
                            <option value="nature">自然主題</option>
                            <option value="ocean">海洋主題</option>
                            <option value="sunset">夕陽主題</option>
                        </select>
                    </div>

                    <div class="theme-preview" :class="`theme-${selectedTheme}`">
                        <div class="preview-header">
                            <h4>{{ getThemeName(selectedTheme) }}</h4>
                        </div>
                        <div class="preview-content">
                            <p>這是 {{ getThemeName(selectedTheme) }} 的預覽效果</p>
                            <button class="preview-button">範例按鈕</button>
                        </div>
                    </div>
                </div>
            </div>

            <div class="code-example">
                <pre v-pre><code>&lt;!-- 自訂樣式的下拉框 --&gt;
&lt;select v-model="selectedTheme" class="custom-select"&gt;
  &lt;option value="light"&gt;淺色主題&lt;/option&gt;
  &lt;option value="dark"&gt;深色主題&lt;/option&gt;
&lt;/select&gt;

// CSS 自訂樣式
.custom-select {
  appearance: none;
  background: url('data:image/svg+xml...') no-repeat right;
  padding: 10px 40px 10px 15px;
}</code></pre>
            </div>
        </div>

        <!-- 數據摘要 -->
        <div class="demo-section">
            <h3>5. 數據摘要</h3>
            <div class="summary-section">
                <h4>當前所有選擇的數據：</h4>
                <div class="data-summary">
                    <pre>{{ formattedSummary }}</pre>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 單選下拉框
const selectedCity = ref('')
const cities = [
    { id: 'taipei', name: '台北', region: '北部', population: 2600000 },
    { id: 'taichung', name: '台中', region: '中部', population: 2800000 },
    { id: 'kaohsiung', name: '高雄', region: '南部', population: 2700000 },
    { id: 'tainan', name: '台南', region: '南部', population: 1900000 },
    { id: 'taoyuan', name: '桃園', region: '北部', population: 2200000 }
]

const selectedCountry = ref('')

// 多選下拉框
const selectedLanguages = ref([])
const programmingLanguages = [
    { id: 'js', name: 'JavaScript', type: 'frontend' },
    { id: 'ts', name: 'TypeScript', type: 'frontend' },
    { id: 'py', name: 'Python', type: 'backend' },
    { id: 'java', name: 'Java', type: 'backend' },
    { id: 'cs', name: 'C#', type: 'backend' },
    { id: 'go', name: 'Go', type: 'backend' },
    { id: 'rust', name: 'Rust', type: 'general' },
    { id: 'cpp', name: 'C++', type: 'general' }
]

// 動態選項
const selectedCategory = ref('')
const selectedJob = ref('')
const selectedSkills = ref([])

const jobCategories = [
    { id: 'engineering', name: '工程技術' },
    { id: 'design', name: '設計創意' },
    { id: 'marketing', name: '行銷企劃' },
    { id: 'management', name: '管理營運' }
]

const jobs = [
    { id: 'frontend', title: '前端工程師', categoryId: 'engineering', skills: ['HTML', 'CSS', 'JavaScript', 'Vue.js', 'React'] },
    { id: 'backend', title: '後端工程師', categoryId: 'engineering', skills: ['Node.js', 'Python', 'Database', 'API設計'] },
    { id: 'fullstack', title: '全端工程師', categoryId: 'engineering', skills: ['Frontend', 'Backend', 'DevOps'] },
    { id: 'uiux', title: 'UI/UX 設計師', categoryId: 'design', skills: ['Figma', 'Sketch', '使用者研究', '原型設計'] },
    { id: 'graphic', title: '平面設計師', categoryId: 'design', skills: ['Photoshop', 'Illustrator', '品牌設計'] },
    { id: 'digital', title: '數位行銷', categoryId: 'marketing', skills: ['SEO', 'SEM', '社群媒體', '數據分析'] },
    { id: 'product', title: '產品經理', categoryId: 'management', skills: ['產品策略', '專案管理', '數據分析'] }
]

// 主題選擇
const selectedTheme = ref('light')

// 計算屬性
const availableJobs = computed(() => {
    if (!selectedCategory.value) return []
    return jobs.filter(job => job.categoryId === selectedCategory.value)
})

const requiredSkills = computed(() => {
    if (!selectedJob.value) return []
    const job = jobs.find(j => j.id === selectedJob.value)
    return job ? job.skills : []
})

const formattedSummary = computed(() => {
    return JSON.stringify({
        城市: selectedCity.value,
        國家: selectedCountry.value,
        程式語言: selectedLanguages.value,
        職業類別: selectedCategory.value,
        職業: selectedJob.value,
        技能: selectedSkills.value,
        主題: selectedTheme.value
    }, null, 2)
})

// 方法
const getCityInfo = (cityId) => {
    return cities.find(city => city.id === cityId)
}

const getLanguageName = (langId) => {
    const lang = programmingLanguages.find(l => l.id === langId)
    return lang ? lang.name : langId
}

const countLanguagesByType = (type) => {
    return selectedLanguages.value.filter(langId => {
        const lang = programmingLanguages.find(l => l.id === langId)
        return lang && lang.type === type
    }).length
}

const getCategoryName = (categoryId) => {
    const category = jobCategories.find(c => c.id === categoryId)
    return category ? category.name : categoryId
}

const getJobTitle = (jobId) => {
    const job = jobs.find(j => j.id === jobId)
    return job ? job.title : jobId
}

const getThemeName = (themeId) => {
    const themes = {
        light: '淺色主題',
        dark: '深色主題',
        nature: '自然主題',
        ocean: '海洋主題',
        sunset: '夕陽主題'
    }
    return themes[themeId] || themeId
}
</script>
