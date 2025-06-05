<template>
    <div class="self-challenge-solution">
        <h2>✅ 自我試煉解答 - Reactivity 響應式</h2>
        <p class="route-info">📍 路徑：/ReactivitySamples/SelfChallengeSolution.vue</p>
        <p class="description">
            📝 <strong>解答版本：</strong>完整實現 Vue 3 響應式系統的各種功能
        </p>

        <!-- 任務狀態 -->
        <div class="task-status">
            <h3>🎯 完成狀態</h3>
            <div class="completed-tasks">
                <span class="task-badge completed">✅ 基本 ref 響應式變數</span>
                <span class="task-badge completed">✅ reactive 物件響應式</span>
                <span class="task-badge completed">✅ 深層響應式運作</span>
                <span class="task-badge completed">✅ computed 響應式計算</span>
                <span class="task-badge completed">✅ 響應式陣列操作</span>
                <span class="task-badge completed">✅ 用戶資料管理系統</span>
            </div>
        </div>

        <!-- 功能展示區域 -->
        <div class="demo-section">
            <h3>🎬 功能展示</h3>

            <!-- 基本 ref 變數 -->
            <div class="demo-card">
                <h4>1. 基本 ref 響應式變數</h4>
                <div class="demo-content">
                    <p><strong>姓名：</strong>{{ name }}</p>
                    <p><strong>年齡：</strong>{{ age }}</p>
                    <p><strong>是否為學生：</strong>{{ isStudent ? '是' : '否' }}</p>
                    <p><strong>興趣：</strong>{{ hobbies.join(', ') }}</p>

                    <div class="controls">
                        <input v-model="name" placeholder="修改姓名" />
                        <input v-model.number="age" type="number" placeholder="修改年齡" />
                        <label>
                            <input type="checkbox" v-model="isStudent" />
                            學生身分
                        </label>
                        <button @click="addHobby">新增興趣</button>
                    </div>
                </div>
            </div>

            <!-- reactive 物件 -->
            <div class="demo-card">
                <h4>2. Reactive 物件響應式</h4>
                <div class="demo-content">
                    <div class="user-profile">
                        <h5>用戶資料</h5>
                        <p><strong>姓名：</strong>{{ userProfile.name }}</p>
                        <p><strong>信箱：</strong>{{ userProfile.email }}</p>
                        <p><strong>頭像：</strong>{{ userProfile.avatar }}</p>
                    </div>

                    <div class="user-settings">
                        <h5>系統設定</h5>
                        <p><strong>主題：</strong>{{ settings.theme }}</p>
                        <p><strong>語言：</strong>{{ settings.language }}</p>
                        <p><strong>通知：</strong>{{ settings.notifications ? '開啟' : '關閉' }}</p>
                    </div>

                    <div class="user-stats">
                        <h5>統計資訊</h5>
                        <p><strong>登入次數：</strong>{{ stats.loginCount }}</p>
                        <p><strong>最後登入：</strong>{{ stats.lastLoginTime }}</p>
                        <p><strong>分數：</strong>{{ stats.score }}</p>
                    </div>

                    <div class="controls">
                        <input v-model="userProfile.name" placeholder="用戶名稱" />
                        <input v-model="userProfile.email" placeholder="電子信箱" />
                        <select v-model="settings.theme">
                            <option value="light">淺色主題</option>
                            <option value="dark">深色主題</option>
                        </select>
                        <label>
                            <input type="checkbox" v-model="settings.notifications" />
                            開啟通知
                        </label>
                        <button @click="updateStats">更新統計</button>
                    </div>
                </div>
            </div>

            <!-- 用戶名稱更新 -->
            <div class="demo-card">
                <h4>3. 用戶名稱更新功能</h4>
                <div class="demo-content">
                    <p><strong>當前名稱：</strong>{{ name }} / {{ userProfile.name }}</p>
                    <div class="controls">
                        <input v-model="newUserName" placeholder="輸入新名稱" />
                        <button @click="updateUserName(newUserName)">更新名稱</button>
                    </div>
                    <div v-if="updateMessage" class="message">{{ updateMessage }}</div>
                </div>
            </div>

            <!-- 計算屬性展示 -->
            <div class="demo-card">
                <h4>4. 計算屬性 - 用戶顯示名稱</h4>
                <div class="demo-content">
                    <p class="display-name">{{ userDisplayName }}</p>
                    <p class="description">這個顯示名稱會根據姓名、年齡和學生身分自動更新</p>
                </div>
            </div>

            <!-- 響應式陣列操作 -->
            <div class="demo-card">
                <h4>5. 響應式陣列操作</h4>
                <div class="demo-content">
                    <p><strong>興趣列表：</strong></p>
                    <ul>
                        <li v-for="(hobby, index) in hobbies" :key="index">
                            {{ hobby }}
                            <button @click="removeHobby(index)">移除</button>
                        </li>
                    </ul>
                    <div class="controls">
                        <input v-model="newHobby" placeholder="新增興趣" @keyup.enter="addNewHobby" />
                        <button @click="addNewHobby">新增</button>
                        <button @click="clearHobbies">清空全部</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, reactive, computed } from 'vue'

// 1. 基本 ref 變數
const name = ref('小明')
const age = ref(25)
const isStudent = ref(true)
const hobbies = ref(['讀書', '運動'])

// 2. reactive 物件
const userProfile = reactive({
    name: '小明',
    email: 'xiaoming@example.com',
    avatar: 'https://i.pravatar.cc/150?u=xiaoming'
})

const settings = reactive({
    theme: 'light',
    language: 'zh-TW',
    notifications: true
})

const stats = reactive({
    loginCount: 12,
    lastLoginTime: new Date().toLocaleString(),
    score: 85
})

// 輔助變數
const newUserName = ref('')
const updateMessage = ref('')
const newHobby = ref('')

// 3. updateUserName(newName) 函數
const updateUserName = (newName) => {
    // 驗證名稱
    if (!newName || newName.trim().length < 2 || newName.trim().length > 20) {
        updateMessage.value = '名稱長度需在 2-20 字元之間'
        setTimeout(() => updateMessage.value = '', 3000)
        return
    }

    // 更新 ref 和 reactive
    name.value = newName.trim()
    userProfile.name = newName.trim()

    // 更新時間戳
    stats.lastLoginTime = new Date().toLocaleString()

    updateMessage.value = '用戶名稱更新成功！'
    newUserName.value = ''
    setTimeout(() => updateMessage.value = '', 3000)
}

// 4. userDisplayName 計算屬性
const userDisplayName = computed(() => {
    let displayName = `${name.value} (${age.value}歲)`
    if (isStudent.value) {
        displayName += ' (學生)'
    }
    return displayName
})

// 陣列操作函數
const addHobby = () => {
    const newHobby = `興趣${hobbies.value.length + 1}`
    hobbies.value.push(newHobby)
}

const addNewHobby = () => {
    if (newHobby.value.trim()) {
        hobbies.value.push(newHobby.value.trim())
        newHobby.value = ''
    }
}

const removeHobby = (index) => {
    hobbies.value.splice(index, 1)
}

const clearHobbies = () => {
    hobbies.value = []
}

// 更新統計函數
const updateStats = () => {
    stats.loginCount++
    stats.score = Math.min(stats.score + 5, 100)
    stats.lastLoginTime = new Date().toLocaleString()
}
</script>

<style scoped>
.self-challenge-solution {
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.route-info {
    color: #666;
    font-size: 0.9em;
    margin-bottom: 10px;
}

.description {
    color: #2c3e50;
    margin-bottom: 30px;
    font-size: 1.1em;
}

.task-status {
    background: #f8f9fa;
    padding: 20px;
    border-radius: 10px;
    margin-bottom: 30px;
    border-left: 4px solid #28a745;
}

.completed-tasks {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    margin-top: 15px;
}

.task-badge {
    padding: 8px 16px;
    border-radius: 20px;
    font-size: 0.9em;
    font-weight: 500;
}

.task-badge.completed {
    background: #d4edda;
    color: #155724;
    border: 1px solid #c3e6cb;
}

.demo-section {
    display: grid;
    gap: 20px;
}

.demo-card {
    background: white;
    border: 1px solid #e9ecef;
    border-radius: 10px;
    padding: 20px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    transition: transform 0.2s;
}

.demo-card:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
}

.demo-card h4 {
    color: #495057;
    margin-bottom: 15px;
    padding-bottom: 10px;
    border-bottom: 2px solid #e9ecef;
}

.demo-content {
    display: flex;
    flex-direction: column;
    gap: 15px;
}

.user-profile,
.user-settings,
.user-stats {
    background: #f8f9fa;
    padding: 15px;
    border-radius: 8px;
    border-left: 4px solid #007bff;
}

.controls {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    align-items: center;
    margin-top: 15px;
}

.controls input,
.controls select {
    padding: 8px 12px;
    border: 1px solid #ced4da;
    border-radius: 5px;
    font-size: 0.9em;
}

.controls button {
    padding: 8px 16px;
    background: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background 0.2s;
}

.controls button:hover {
    background: #0056b3;
}

.display-name {
    font-size: 1.3em;
    font-weight: bold;
    color: #495057;
    text-align: center;
    padding: 15px;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    border-radius: 10px;
}

.message {
    padding: 10px 15px;
    background: #d1ecf1;
    color: #0c5460;
    border: 1px solid #bee5eb;
    border-radius: 5px;
    margin-top: 10px;
}

ul {
    list-style: none;
    padding: 0;
}

li {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 8px 12px;
    background: #f8f9fa;
    margin-bottom: 5px;
    border-radius: 5px;
}

li button {
    background: #dc3545;
    color: white;
    border: none;
    padding: 4px 8px;
    border-radius: 3px;
    cursor: pointer;
    font-size: 0.8em;
}

li button:hover {
    background: #c82333;
}

@media (max-width: 768px) {
    .controls {
        flex-direction: column;
        align-items: stretch;
    }

    .completed-tasks {
        flex-direction: column;
    }
}
</style>
