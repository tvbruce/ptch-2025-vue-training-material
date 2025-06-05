<template>
    <div class="self-challenge">
        <h2>🎯 自我試煉解答 - v-if 條件渲染</h2>
        <p class="route-info">📍 路徑：/ConditionalSamples/SelfChallengeSolution.vue</p>
        <p class="description">
            ✅ <strong>完整解答：</strong>智能內容管理系統條件渲染完整實作範例
        </p>

        <div class="solution-overview">
            <h3>📋 解答概覽</h3>
            <div class="feature-list">
                <div class="feature-item completed">
                    <span class="icon">✅</span>
                    <span>多重條件 v-if、v-else-if、v-else</span>
                </div>
                <div class="feature-item completed">
                    <span class="icon">✅</span>
                    <span>v-show 頻繁切換內容</span>
                </div>
                <div class="feature-item completed">
                    <span class="icon">✅</span>
                    <span>template 標籤包裝多個元素</span>
                </div>
                <div class="feature-item completed">
                    <span class="icon">✅</span>
                    <span>複雜條件邏輯組合</span>
                </div>
                <div class="feature-item completed">
                    <span class="icon">✅</span>
                    <span>條件渲染與列表渲染結合</span>
                </div>
                <div class="feature-item completed">
                    <span class="icon">✅</span>
                    <span>用戶權限管理系統</span>
                </div>
            </div>
        </div>

        <!-- 用戶狀態控制面板 -->
        <div class="control-panel">
            <h3>🎛️ 用戶狀態控制</h3>
            <div class="user-controls">
                <div class="control-group">
                    <label>登入狀態：</label>
                    <label class="radio-label">
                        <input type="radio" :value="true" v-model="isLoggedIn">
                        已登入
                    </label>
                    <label class="radio-label">
                        <input type="radio" :value="false" v-model="isLoggedIn">
                        未登入
                    </label>
                </div>

                <div class="control-group" v-show="isLoggedIn">
                    <label>用戶類型：</label>
                    <select v-model="userType" class="select-field">
                        <option value="user">一般用戶</option>
                        <option value="vip">VIP用戶</option>
                        <option value="admin">管理員</option>
                    </select>
                </div>

                <div class="control-group" v-show="isLoggedIn">
                    <label class="checkbox-label">
                        <input type="checkbox" v-model="hasSpecialPermission">
                        特殊權限
                    </label>
                    <label class="checkbox-label">
                        <input type="checkbox" v-model="isAccountActive">
                        帳號啟用
                    </label>
                </div>

                <div class="control-group">
                    <label class="checkbox-label">
                        <input type="checkbox" v-model="showDebugInfo">
                        顯示調試資訊
                    </label>
                </div>
            </div>
        </div>

        <!-- 歡迎區塊 - 基本條件渲染 -->
        <div class="welcome-section">
            <h3>👋 歡迎區塊（基本條件渲染）</h3>

            <!-- 使用 v-if 進行條件渲染 -->
            <div v-if="shouldShowWelcome" class="welcome-card welcome">
                <h4>{{ getUserTypeMessage }}</h4>
                <p>當前時間：{{ currentTime }}</p>
                <template v-if="isLoggedIn">
                    <p>用戶類型：{{ userType.toUpperCase() }}</p>
                    <p>帳號狀態：{{ isAccountActive ? '正常' : '待啟用' }}</p>
                    <div v-if="hasSpecialPermission" class="special-badge">
                        🌟 特殊權限用戶
                    </div>
                </template>
            </div>

            <!-- 使用 v-else 顯示替代內容 -->
            <div v-else class="welcome-card guest">
                <h4>歡迎訪客</h4>
                <p>請登入以獲得完整體驗</p>
                <button @click="simulateLogin" class="btn-primary">模擬登入</button>
            </div>
        </div>

        <!-- 功能導航 - 多重條件渲染 -->
        <div class="navigation-section">
            <h3>🧭 功能導航（多重條件渲染）</h3>

            <!-- 根據用戶類型顯示不同導航 -->
            <div v-if="!isLoggedIn" class="nav-card guest-nav">
                <h4>訪客功能</h4>
                <ul>
                    <li>📖 瀏覽公開內容</li>
                    <li>👤 註冊帳號</li>
                    <li>❓ 查看幫助</li>
                </ul>
            </div>

            <div v-else-if="userType === 'user'" class="nav-card user-nav">
                <h4>一般用戶功能</h4>
                <ul>
                    <li>👤 個人資料管理</li>
                    <li>💬 發表評論</li>
                    <li>⭐ 收藏內容</li>
                    <li>📊 個人統計</li>
                </ul>
            </div>

            <div v-else-if="userType === 'vip'" class="nav-card vip-nav">
                <h4>VIP 用戶功能</h4>
                <ul>
                    <li>👤 個人資料管理</li>
                    <li>💬 發表評論</li>
                    <li>⭐ 收藏內容</li>
                    <li>📥 下載資源</li>
                    <li>🎯 優先客服</li>
                    <li>💎 VIP專區</li>
                </ul>
            </div>

            <div v-else-if="userType === 'admin'" class="nav-card admin-nav">
                <h4>管理員功能</h4>
                <ul>
                    <li>👥 用戶管理</li>
                    <li>⚙️ 系統設定</li>
                    <li>📈 數據統計</li>
                    <li>🔧 開發工具</li>
                    <li>🛡️ 安全監控</li>
                </ul>
            </div>
        </div>

        <!-- 動態功能列表 - 條件渲染與列表結合 -->
        <div class="features-section">
            <h3>⚡ 可用功能（動態列表）</h3>

            <template v-if="isLoading">
                <div class="loading-card">
                    <div class="spinner"></div>
                    <p>正在載入功能列表...</p>
                </div>
            </template>

            <template v-else-if="getAvailableFeatures.length > 0">
                <div class="features-grid">
                    <div v-for="feature in getAvailableFeatures" :key="feature.name" class="feature-card" :class="{
                        'premium': feature.isPremium,
                        'admin-only': feature.isAdminOnly
                    }">
                        <div class="feature-icon">{{ feature.icon }}</div>
                        <h5>{{ feature.name }}</h5>
                        <p>{{ feature.description }}</p>
                        <div v-if="feature.isPremium" class="premium-badge">
                            💎 進階功能
                        </div>
                    </div>
                </div>
            </template>

            <template v-else>
                <div class="empty-state">
                    <div class="empty-icon">🚫</div>
                    <h4>暫無可用功能</h4>
                    <p>請登入或升級帳號以獲得更多功能</p>
                </div>
            </template>
        </div>

        <!-- 標籤頁系統 - v-show 示例 -->
        <div class="tabs-section">
            <h3>📑 標籤頁系統（v-show 示例）</h3>

            <div class="tab-buttons">
                <button v-for="tab in tabs" :key="tab.id" @click="activeTab = tab.id"
                    :class="{ active: activeTab === tab.id }" class="tab-button">
                    {{ tab.label }}
                </button>
            </div>

            <div class="tab-contents">
                <!-- 使用 v-show 提高切換性能 -->
                <div v-show="activeTab === 'profile'" class="tab-content">
                    <h4>個人資料</h4>
                    <div v-if="isLoggedIn" class="profile-info">
                        <p>用戶類型：{{ userType }}</p>
                        <p>特殊權限：{{ hasSpecialPermission ? '是' : '否' }}</p>
                        <p>帳號狀態：{{ isAccountActive ? '正常' : '待啟用' }}</p>
                    </div>
                    <div v-else class="login-prompt">
                        <p>請先登入查看個人資料</p>
                    </div>
                </div>

                <div v-show="activeTab === 'settings'" class="tab-content">
                    <h4>系統設定</h4>
                    <div v-if="canAccessFeature('settings')" class="settings-content">
                        <label class="checkbox-label">
                            <input type="checkbox" v-model="settings.notifications">
                            啟用通知
                        </label>
                        <label class="checkbox-label">
                            <input type="checkbox" v-model="settings.darkMode">
                            深色模式
                        </label>
                        <div v-if="userType === 'admin'" class="admin-settings">
                            <h5>管理員設定</h5>
                            <label class="checkbox-label">
                                <input type="checkbox" v-model="settings.debugMode">
                                調試模式
                            </label>
                        </div>
                    </div>
                    <div v-else class="access-denied">
                        <p>⚠️ 您沒有權限訪問此功能</p>
                    </div>
                </div>

                <div v-show="activeTab === 'help'" class="tab-content">
                    <h4>幫助中心</h4>
                    <div class="help-content">
                        <div class="help-item">
                            <h5>如何登入？</h5>
                            <p>點擊右上角的登入按鈕，輸入您的帳號密碼即可。</p>
                        </div>
                        <div v-if="isLoggedIn" class="help-item">
                            <h5>如何升級為VIP？</h5>
                            <p>前往個人中心，選擇合適的VIP套餐進行升級。</p>
                        </div>
                        <div v-if="userType === 'admin'" class="help-item admin-help">
                            <h5>管理員專區</h5>
                            <p>管理員可以訪問系統設定和用戶管理功能。</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- 模態框 - 條件顯示 -->
        <div class="modal-section">
            <h3>📋 模態框系統</h3>
            <div class="modal-controls">
                <button @click="showModal = true" class="btn-secondary">
                    開啟模態框
                </button>
            </div>
        </div>

        <!-- 模態框組件 -->
        <div v-if="showModal" class="modal-overlay" @click="showModal = false">
            <div class="modal-content" @click.stop>
                <div class="modal-header">
                    <h4>系統訊息</h4>
                    <button @click="showModal = false" class="close-button">×</button>
                </div>
                <div class="modal-body">
                    <template v-if="isLoggedIn">
                        <p>歡迎 {{ userType }} 用戶！</p>
                        <div v-if="hasSpecialPermission" class="special-message">
                            <p>🎉 您擁有特殊權限，可以訪問額外功能！</p>
                        </div>
                        <div v-else>
                            <p>💡 升級帳號可以獲得更多權限喔！</p>
                        </div>
                    </template>
                    <template v-else>
                        <p>請先登入以獲得個人化體驗</p>
                        <button @click="simulateLogin" class="btn-primary">立即登入</button>
                    </template>
                </div>
            </div>
        </div>

        <!-- 調試資訊 -->
        <div v-show="showDebugInfo" class="debug-section">
            <h3>🐛 調試資訊</h3>
            <div class="debug-info">
                <div class="debug-item">
                    <strong>isLoggedIn:</strong> {{ isLoggedIn }}
                </div>
                <div class="debug-item">
                    <strong>userType:</strong> {{ userType }}
                </div>
                <div class="debug-item">
                    <strong>hasSpecialPermission:</strong> {{ hasSpecialPermission }}
                </div>
                <div class="debug-item">
                    <strong>isAccountActive:</strong> {{ isAccountActive }}
                </div>
                <div class="debug-item">
                    <strong>shouldShowWelcome:</strong> {{ shouldShowWelcome }}
                </div>
                <div class="debug-item">
                    <strong>availableFeatures:</strong> {{ getAvailableFeatures.length }} 項
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, reactive, computed, onMounted, onUnmounted } from 'vue'

// ===== 基本響應式資料 =====
const isLoggedIn = ref(false)
const userType = ref('user')
const hasSpecialPermission = ref(false)
const isAccountActive = ref(true)
const showDebugInfo = ref(false)
const isLoading = ref(false)
const showModal = ref(false)
const activeTab = ref('profile')
const currentTime = ref(new Date().toLocaleString())

// 設定資料
const settings = reactive({
    notifications: true,
    darkMode: false,
    debugMode: false
})

// 標籤頁配置
const tabs = [
    { id: 'profile', label: '個人資料' },
    { id: 'settings', label: '系統設定' },
    { id: 'help', label: '幫助中心' }
]

// 時間更新定時器
let timeTimer = null

// ===== 計算屬性 =====

// 1. 是否顯示歡迎訊息
const shouldShowWelcome = computed(() => {
    // 可以加入時間邏輯，例如工作時間
    const hour = new Date().getHours()
    const isWorkingHours = hour >= 9 && hour <= 18

    // 登入用戶或工作時間內都顯示歡迎訊息
    return isLoggedIn.value || isWorkingHours
})

// 2. 用戶類型歡迎訊息
const getUserTypeMessage = computed(() => {
    if (!isLoggedIn.value) {
        return '歡迎訪客，請先登入以獲得完整體驗'
    }

    switch (userType.value) {
        case 'user':
            return '歡迎回來！希望您今天過得愉快'
        case 'vip':
            return '歡迎尊貴的VIP用戶，享受專屬服務'
        case 'admin':
            return '歡迎管理員，您擁有完整的系統權限'
        default:
            return '歡迎使用我們的系統'
    }
})

// 3. 可用功能列表
const getAvailableFeatures = computed(() => {
    const features = []

    if (!isLoggedIn.value) {
        features.push(
            { name: '瀏覽公開內容', description: '查看公開的文章和資源', icon: '📖', isPremium: false, isAdminOnly: false },
            { name: '註冊帳號', description: '建立新的用戶帳號', icon: '👤', isPremium: false, isAdminOnly: false }
        )
    } else {
        // 基本用戶功能
        features.push(
            { name: '個人資料', description: '管理您的個人資訊', icon: '👤', isPremium: false, isAdminOnly: false },
            { name: '發表評論', description: '在文章下方留言評論', icon: '💬', isPremium: false, isAdminOnly: false },
            { name: '收藏內容', description: '收藏喜歡的文章和資源', icon: '⭐', isPremium: false, isAdminOnly: false }
        )

        // VIP 用戶額外功能
        if (userType.value === 'vip' || userType.value === 'admin') {
            features.push(
                { name: '下載資源', description: '下載高品質的檔案資源', icon: '📥', isPremium: true, isAdminOnly: false },
                { name: '優先客服', description: '享受優先的客戶服務', icon: '🎯', isPremium: true, isAdminOnly: false },
                { name: 'VIP專區', description: '訪問VIP專屬內容', icon: '💎', isPremium: true, isAdminOnly: false }
            )
        }

        // 管理員功能
        if (userType.value === 'admin') {
            features.push(
                { name: '用戶管理', description: '管理系統中的所有用戶', icon: '👥', isPremium: false, isAdminOnly: true },
                { name: '系統設定', description: '調整系統各項參數', icon: '⚙️', isPremium: false, isAdminOnly: true },
                { name: '數據統計', description: '查看系統使用統計', icon: '📈', isPremium: false, isAdminOnly: true }
            )
        }

        // 特殊權限功能
        if (hasSpecialPermission.value) {
            features.push(
                { name: '測試功能', description: '體驗最新的實驗性功能', icon: '🧪', isPremium: true, isAdminOnly: false },
                { name: '開發工具', description: '開發者專用的調試工具', icon: '🔧', isPremium: true, isAdminOnly: false }
            )
        }
    }

    return features
})

// ===== 函數實作 =====

// 4. 檢查用戶是否有權限訪問特定功能
const canAccessFeature = (feature) => {
    const featurePermissions = {
        'profile': 'user',
        'settings': 'user',
        'help': 'public',
        'vip-area': 'vip',
        'admin-panel': 'admin',
        'user-management': 'admin',
        'system-config': 'admin'
    }

    const requiredLevel = featurePermissions[feature] || 'public'

    switch (requiredLevel) {
        case 'public':
            return true
        case 'user':
            return isLoggedIn.value && isAccountActive.value
        case 'vip':
            return isLoggedIn.value && isAccountActive.value && (userType.value === 'vip' || userType.value === 'admin')
        case 'admin':
            return isLoggedIn.value && isAccountActive.value && userType.value === 'admin'
        default:
            return false
    }
}

// 模擬登入功能
const simulateLogin = () => {
    isLoggedIn.value = true
    userType.value = 'user'
    isAccountActive.value = true
    showModal.value = false

    // 模擬載入過程
    isLoading.value = true
    setTimeout(() => {
        isLoading.value = false
    }, 1000)
}

// 更新時間
const updateTime = () => {
    currentTime.value = new Date().toLocaleString()
}

// ===== 生命週期 =====
onMounted(() => {
    console.log('條件渲染解答組件已載入')

    // 每秒更新時間
    timeTimer = setInterval(updateTime, 1000)
})

onUnmounted(() => {
    if (timeTimer) {
        clearInterval(timeTimer)
    }
})
</script>

<style scoped>
@import '@/assets/main.css';

.solution-overview {
    background: linear-gradient(135deg, #fff3e0 0%, #e8f5e8 100%);
    padding: 1.5rem;
    border-radius: 8px;
    margin-bottom: 2rem;
    border: 2px solid #FF9800;
}

.feature-list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 0.5rem;
    margin-top: 1rem;
}

.feature-item {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    padding: 0.5rem;
}

.feature-item.completed .icon {
    color: #4CAF50;
    font-weight: bold;
}

/* 控制面板樣式 */
.control-panel {
    background: #f8f9fa;
    padding: 1.5rem;
    border-radius: 8px;
    margin-bottom: 2rem;
    border: 1px solid #ddd;
}

.user-controls {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1rem;
}

.control-group {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    flex-wrap: wrap;
}

.control-group label {
    font-weight: 500;
    min-width: 80px;
}

.radio-label,
.checkbox-label {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    cursor: pointer;
    font-weight: normal !important;
    min-width: auto !important;
}

.select-field {
    padding: 0.5rem;
    border: 1px solid #ddd;
    border-radius: 4px;
}

/* 歡迎區塊樣式 */
.welcome-section {
    margin-bottom: 2rem;
}

.welcome-card {
    padding: 1.5rem;
    border-radius: 8px;
    margin-bottom: 1rem;
    border: 2px solid;
}

.welcome-card.welcome {
    background: linear-gradient(135deg, #e8f5e8 0%, #c8e6c9 100%);
    border-color: #4CAF50;
}

.welcome-card.guest {
    background: linear-gradient(135deg, #e3f2fd 0%, #bbdefb 100%);
    border-color: #2196F3;
}

.special-badge {
    background: #FF9800;
    color: white;
    padding: 0.5rem 1rem;
    border-radius: 20px;
    display: inline-block;
    margin-top: 0.5rem;
    font-weight: bold;
}

/* 導航區塊樣式 */
.navigation-section {
    margin-bottom: 2rem;
}

.nav-card {
    padding: 1.5rem;
    border-radius: 8px;
    border: 2px solid;
    background: white;
}

.nav-card.guest-nav {
    border-color: #6c757d;
}

.nav-card.user-nav {
    border-color: #007bff;
}

.nav-card.vip-nav {
    border-color: #FF9800;
    background: linear-gradient(135deg, #fff8e1 0%, #ffecb3 100%);
}

.nav-card.admin-nav {
    border-color: #dc3545;
    background: linear-gradient(135deg, #ffebee 0%, #ffcdd2 100%);
}

.nav-card ul {
    list-style: none;
    padding: 0;
    margin: 0.5rem 0 0 0;
}

.nav-card li {
    padding: 0.5rem 0;
    border-bottom: 1px solid rgba(0, 0, 0, 0.1);
}

.nav-card li:last-child {
    border-bottom: none;
}

/* 功能列表樣式 */
.features-section {
    margin-bottom: 2rem;
}

.loading-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 2rem;
    background: #f8f9fa;
    border-radius: 8px;
}

.spinner {
    width: 40px;
    height: 40px;
    border: 4px solid #f3f3f3;
    border-top: 4px solid #007bff;
    border-radius: 50%;
    animation: spin 1s linear infinite;
    margin-bottom: 1rem;
}

@keyframes spin {
    0% {
        transform: rotate(0deg);
    }

    100% {
        transform: rotate(360deg);
    }
}

.features-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 1rem;
}

.feature-card {
    background: white;
    border: 2px solid #ddd;
    border-radius: 8px;
    padding: 1rem;
    text-align: center;
    transition: transform 0.2s, box-shadow 0.2s;
}

.feature-card:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.feature-card.premium {
    border-color: #FF9800;
    background: linear-gradient(135deg, #fff8e1 0%, #ffecb3 100%);
}

.feature-card.admin-only {
    border-color: #dc3545;
    background: linear-gradient(135deg, #ffebee 0%, #ffcdd2 100%);
}

.feature-icon {
    font-size: 2rem;
    margin-bottom: 0.5rem;
}

.premium-badge {
    background: #FF9800;
    color: white;
    padding: 0.25rem 0.5rem;
    border-radius: 20px;
    font-size: 0.8rem;
    margin-top: 0.5rem;
    display: inline-block;
}

.empty-state {
    text-align: center;
    padding: 3rem;
    background: #f8f9fa;
    border-radius: 8px;
    color: #6c757d;
}

.empty-icon {
    font-size: 3rem;
    margin-bottom: 1rem;
}

/* 標籤頁樣式 */
.tabs-section {
    margin-bottom: 2rem;
}

.tab-buttons {
    display: flex;
    border-bottom: 2px solid #ddd;
    margin-bottom: 1rem;
}

.tab-button {
    padding: 0.75rem 1.5rem;
    border: none;
    background: none;
    cursor: pointer;
    border-bottom: 3px solid transparent;
    transition: all 0.2s;
}

.tab-button:hover {
    background: #f8f9fa;
}

.tab-button.active {
    border-bottom-color: #007bff;
    color: #007bff;
    font-weight: bold;
}

.tab-content {
    background: white;
    padding: 1.5rem;
    border-radius: 8px;
    border: 1px solid #ddd;
    min-height: 200px;
}

.profile-info,
.settings-content,
.help-content {
    line-height: 1.6;
}

.admin-settings {
    margin-top: 1rem;
    padding: 1rem;
    background: #fff3cd;
    border-radius: 4px;
    border: 1px solid #ffeaa7;
}

.access-denied {
    text-align: center;
    color: #dc3545;
    font-weight: bold;
}

.login-prompt {
    text-align: center;
    color: #6c757d;
}

.help-item {
    margin-bottom: 1.5rem;
    padding-bottom: 1rem;
    border-bottom: 1px solid #eee;
}

.help-item:last-child {
    border-bottom: none;
}

.help-item h5 {
    color: #007bff;
    margin-bottom: 0.5rem;
}

.admin-help {
    background: #ffebee;
    padding: 1rem;
    border-radius: 4px;
}

/* 模態框樣式 */
.modal-section {
    margin-bottom: 2rem;
}

.modal-controls {
    text-align: center;
}

.modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000;
}

.modal-content {
    background: white;
    border-radius: 8px;
    max-width: 500px;
    width: 90%;
    max-height: 90vh;
    overflow-y: auto;
}

.modal-header {
    padding: 1rem 1.5rem;
    border-bottom: 1px solid #ddd;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.modal-body {
    padding: 1.5rem;
}

.close-button {
    background: none;
    border: none;
    font-size: 1.5rem;
    cursor: pointer;
    color: #999;
}

.close-button:hover {
    color: #333;
}

.special-message {
    background: #e8f5e8;
    padding: 1rem;
    border-radius: 4px;
    border: 1px solid #4CAF50;
    margin-top: 1rem;
}

/* 調試區塊樣式 */
.debug-section {
    background: #212529;
    color: #fff;
    padding: 1.5rem;
    border-radius: 8px;
    font-family: 'Courier New', monospace;
}

.debug-info {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 0.5rem;
}

.debug-item {
    padding: 0.5rem;
    background: #343a40;
    border-radius: 4px;
}

/* 按鈕樣式 */
.btn-primary {
    background: #007bff;
    color: white;
    border: none;
    padding: 0.5rem 1rem;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s;
}

.btn-primary:hover {
    background: #0056b3;
}

.btn-secondary {
    background: #6c757d;
    color: white;
    border: none;
    padding: 0.5rem 1rem;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s;
}

.btn-secondary:hover {
    background: #545b62;
}
</style>
