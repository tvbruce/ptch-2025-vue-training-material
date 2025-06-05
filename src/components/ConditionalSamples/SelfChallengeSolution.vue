<template>
    <div class="solution">
        <h2>✅ 解答 - v-if 條件渲染</h2>
        <p>完整實現動態內容管理系統，展示各種條件渲染技巧</p>

        <!-- 用戶狀態展示 -->
        <div class="demo-card">
            <h4>用戶狀態管理</h4>
            <div v-if="userStatus === 'guest'" class="status-card guest">
                <h5>訪客模式</h5>
                <p>您尚未登入，請先登入以享受完整功能</p>
                <button @click="toggleLogin">立即登入</button>
            </div>

            <div v-else-if="userStatus === 'user'" class="status-card user">
                <h5>一般用戶</h5>
                <p>歡迎回來，{{ user.name }}！</p>
                <p>您可以使用基本功能</p>
                <button @click="updateUserRole('admin')">升級為管理員</button>
                <button @click="updateUserRole('vip')">升級為 VIP</button>
            </div>

            <div v-else-if="userStatus === 'admin'" class="status-card admin">
                <h5>管理員</h5>
                <p>管理員 {{ user.name }}，您擁有完整權限</p>
                <p>可以存取所有功能和設定</p>
                <button @click="updateUserRole('user')">降級為一般用戶</button>
            </div>

            <div v-else-if="userStatus === 'vip'" class="status-card vip">
                <h5>VIP 用戶</h5>
                <p>VIP 用戶 {{ user.name }}，享受專屬服務</p>
                <p>可以使用進階功能</p>
                <button @click="updateUserRole('user')">降級為一般用戶</button>
            </div>

            <button @click="toggleLogin" class="logout-btn">
                {{ user.isLoggedIn ? '登出' : '登入' }}
            </button>
        </div>

        <!-- 功能權限檢查 -->
        <div class="demo-card">
            <h4>功能權限檢查</h4>
            <div class="feature-list">
                <div class="feature-item">
                    <span>基本功能</span>
                    <span v-if="canAccess('basic')" class="access granted">✅ 可存取</span>
                    <span v-else class="access denied">❌ 無權限</span>
                </div>
                <div class="feature-item">
                    <span>進階功能</span>
                    <span v-if="canAccess('premium')" class="access granted">✅ 可存取</span>
                    <span v-else class="access denied">❌ 無權限</span>
                </div>
                <div class="feature-item">
                    <span>管理功能</span>
                    <span v-if="canAccess('admin')" class="access granted">✅ 可存取</span>
                    <span v-else class="access denied">❌ 無權限</span>
                </div>
            </div>
        </div>

        <!-- 標籤頁切換 -->
        <div class="demo-card">
            <h4>標籤頁切換</h4>
            <div class="tab-navigation">
                <button v-for="tab in tabs" :key="tab" @click="switchTab(tab)" :class="{ active: activeTab === tab }">
                    {{ tabNames[tab] }}
                </button>
            </div>

            <div class="tab-content">
                <div v-if="activeTab === 'home'" class="tab-panel">
                    <h5>首頁</h5>
                    <p>歡迎來到我們的網站！這裡是首頁內容。</p>
                </div>

                <div v-else-if="activeTab === 'about'" class="tab-panel">
                    <h5>關於我們</h5>
                    <p>我們是一家專業的軟體開發公司。</p>
                </div>

                <div v-else-if="activeTab === 'contact'" class="tab-panel">
                    <h5>聯絡我們</h5>
                    <p>Email: contact@example.com</p>
                    <p>電話: (02) 1234-5678</p>
                </div>

                <div v-else-if="activeTab === 'settings'" class="tab-panel">
                    <h5>設定</h5>
                    <template v-if="user.isLoggedIn">
                        <p>用戶設定選項</p>
                        <label>
                            <input type="checkbox" v-model="user.notifications" />
                            接收通知
                        </label>
                    </template>
                    <p v-else>請先登入以存取設定</p>
                </div>
            </div>
        </div>

        <!-- v-show 展示 -->
        <div class="demo-card">
            <h4>v-show 頻繁切換</h4>
            <button @click="toggleModal">
                {{ showModal ? '關閉' : '開啟' }}模態框
            </button>

            <div v-show="showModal" class="modal-overlay">
                <div class="modal-content">
                    <h5>模態框內容</h5>
                    <p>這是使用 v-show 控制的模態框，適合頻繁切換顯示</p>
                    <button @click="toggleModal">關閉</button>
                </div>
            </div>
        </div>

        <!-- 複雜條件邏輯 -->
        <div class="demo-card">
            <h4>複雜條件邏輯</h4>
            <div class="user-info">
                <p><strong>當前狀態：</strong>{{ userStatus }}</p>
                <p><strong>登入狀態：</strong>{{ user.isLoggedIn ? '已登入' : '未登入' }}</p>
                <p><strong>用戶角色：</strong>{{ user.role }}</p>
                <p><strong>用戶名稱：</strong>{{ user.name || '未設定' }}</p>
            </div>

            <div class="condition-display">
                <p v-if="user.isLoggedIn && user.role === 'admin'">
                    🔧 管理員專用控制面板
                </p>
                <p v-else-if="user.isLoggedIn && user.role === 'vip'">
                    ⭐ VIP 專屬功能區
                </p>
                <p v-else-if="user.isLoggedIn">
                    👤 用戶個人中心
                </p>
                <p v-else>
                    🚪 請登入以存取更多功能
                </p>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, reactive, computed } from 'vue'

// 用戶資料
const user = reactive({
    isLoggedIn: false,
    name: '',
    role: 'user',
    notifications: true
})

// 介面狀態
const activeTab = ref('home')
const showModal = ref(false)

// 標籤頁設定
const tabs = ['home', 'about', 'contact', 'settings']
const tabNames = {
    home: '首頁',
    about: '關於我們',
    contact: '聯絡我們',
    settings: '設定'
}

// 1. userStatus 計算屬性
const userStatus = computed(() => {
    if (!user.isLoggedIn) {
        return 'guest'
    }
    return user.role
})

// 2. toggleLogin 函數
const toggleLogin = () => {
    user.isLoggedIn = !user.isLoggedIn

    if (user.isLoggedIn) {
        user.name = '用戶' + Math.floor(Math.random() * 1000)
    } else {
        user.role = 'user'
        user.name = ''
    }
}

// 3. switchTab 函數
const switchTab = (tabName) => {
    if (tabs.includes(tabName)) {
        activeTab.value = tabName
    }
}

// 4. toggleModal 函數
const toggleModal = () => {
    showModal.value = !showModal.value
}

// 5. updateUserRole 函數
const updateUserRole = (role) => {
    if (user.isLoggedIn && ['user', 'admin', 'vip'].includes(role)) {
        user.role = role
    }
}

// 6. canAccess 函數
const canAccess = (feature) => {
    if (!user.isLoggedIn) return false

    switch (feature) {
        case 'basic':
            return true // 所有已登入用戶
        case 'premium':
            return user.role === 'vip' || user.role === 'admin'
        case 'admin':
            return user.role === 'admin'
        default:
            return false
    }
}
</script>

<style scoped>
.solution {
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
}

.demo-card {
    background: white;
    border: 1px solid #e9ecef;
    border-radius: 10px;
    padding: 20px;
    margin-bottom: 20px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.status-card {
    padding: 20px;
    border-radius: 10px;
    margin: 15px 0;
    text-align: center;
}

.status-card.guest {
    background: linear-gradient(135deg, #f8f9fa, #e9ecef);
    border-left: 4px solid #6c757d;
}

.status-card.user {
    background: linear-gradient(135deg, #e3f2fd, #bbdefb);
    border-left: 4px solid #2196f3;
}

.status-card.admin {
    background: linear-gradient(135deg, #fff3e0, #ffcc02);
    border-left: 4px solid #ff9800;
}

.status-card.vip {
    background: linear-gradient(135deg, #f3e5f5, #e1bee7);
    border-left: 4px solid #9c27b0;
}

.feature-list {
    display: grid;
    gap: 10px;
}

.feature-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 15px;
    background: #f8f9fa;
    border-radius: 5px;
}

.access.granted {
    color: #28a745;
    font-weight: bold;
}

.access.denied {
    color: #dc3545;
    font-weight: bold;
}

.tab-navigation {
    display: flex;
    gap: 5px;
    margin-bottom: 20px;
    border-bottom: 1px solid #e9ecef;
}

.tab-navigation button {
    padding: 10px 20px;
    border: none;
    background: transparent;
    cursor: pointer;
    border-bottom: 2px solid transparent;
    transition: all 0.2s;
}

.tab-navigation button.active {
    border-bottom-color: #007bff;
    color: #007bff;
    font-weight: bold;
}

.tab-navigation button:hover {
    background: #f8f9fa;
}

.tab-panel {
    min-height: 150px;
    padding: 20px;
    background: #f8f9fa;
    border-radius: 5px;
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
    padding: 30px;
    border-radius: 10px;
    max-width: 500px;
    text-align: center;
}

.user-info {
    background: #f8f9fa;
    padding: 15px;
    border-radius: 5px;
    margin-bottom: 15px;
}

.condition-display {
    padding: 15px;
    border: 2px dashed #007bff;
    border-radius: 5px;
    text-align: center;
    font-weight: bold;
}

button {
    padding: 8px 16px;
    margin: 5px;
    border: 1px solid #007bff;
    background: #007bff;
    color: white;
    border-radius: 5px;
    cursor: pointer;
    transition: background 0.2s;
}

button:hover {
    background: #0056b3;
}

.logout-btn {
    background: #dc3545;
    border-color: #dc3545;
}

.logout-btn:hover {
    background: #c82333;
}
</style>
