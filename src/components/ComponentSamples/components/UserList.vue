<template>
    <div class="user-list">
        <div class="list-header">
            <h4>👥 用戶列表</h4>
            <div class="list-stats">
                <span class="stat-item">總計: {{ users.length }} 人</span>
                <span class="stat-item">管理員: {{ adminCount }} 人</span>
                <span class="stat-item">一般用戶: {{ userCount }} 人</span>
            </div>
        </div>

        <!-- 搜索和篩選 -->
        <div class="list-controls">
            <div class="search-box">
                <input v-model="searchQuery" type="text" placeholder="🔍 搜索用戶..." class="search-input" />
            </div>
            <div class="filter-box">
                <select v-model="roleFilter" class="filter-select">
                    <option value="">所有角色</option>
                    <option value="admin">管理員</option>
                    <option value="user">一般用戶</option>
                    <option value="editor">編輯者</option>
                </select>
            </div>
        </div>

        <!-- 用戶卡片列表 -->
        <div class="user-cards">
            <div v-for="user in filteredUsers" :key="user.id" class="user-card"
                :class="{ editing: editingUser?.id === user.id }">
                <!-- 編輯模式 -->
                <div v-if="editingUser?.id === user.id" class="edit-mode">
                    <div class="edit-header">
                        <h5>✏️ 編輯用戶</h5>
                        <div class="edit-actions">
                            <button @click="saveUser" class="save-btn">💾 保存</button>
                            <button @click="cancelEdit" class="cancel-btn">❌ 取消</button>
                        </div>
                    </div>

                    <div class="edit-form">
                        <div class="edit-group">
                            <label>姓名:</label>
                            <input v-model="editingUser.name" type="text" class="edit-input" />
                        </div>
                        <div class="edit-group">
                            <label>電子郵件:</label>
                            <input v-model="editingUser.email" type="email" class="edit-input" />
                        </div>
                        <div class="edit-group">
                            <label>角色:</label>
                            <select v-model="editingUser.role" class="edit-select">
                                <option value="admin">管理員</option>
                                <option value="user">一般用戶</option>
                                <option value="editor">編輯者</option>
                            </select>
                        </div>
                    </div>
                </div>

                <!-- 顯示模式 -->
                <div v-else class="display-mode">
                    <div class="user-avatar">{{ user.avatar }}</div>

                    <div class="user-info">
                        <div class="user-name">{{ user.name }}</div>
                        <div class="user-email">{{ user.email }}</div>

                        <!-- 使用具名插槽顯示用戶徽章 -->
                        <div class="user-badge-container">
                            <slot name="user-badge" :user="user">
                                <!-- 默認徽章樣式 -->
                                <span class="default-badge" :class="user.role">
                                    {{ user.role === 'admin' ? '��' : '👤' }} {{ user.role }}
                                </span>
                            </slot>
                        </div>

                        <div v-if="user.bio" class="user-bio">{{ user.bio }}</div>
                    </div>

                    <div class="user-actions">
                        <button @click="editUser(user)" class="action-btn edit-btn">
                            ✏️ 編輯
                        </button>
                        <button @click="deleteUser(user.id)" class="action-btn delete-btn">
                            🗑️ 刪除
                        </button>
                        <button @click="toggleUserStatus(user)" class="action-btn status-btn">
                            {{ user.active ? '🔴 停用' : '🟢 啟用' }}
                        </button>
                    </div>
                </div>

                <!-- 用戶詳情展開 -->
                <div v-if="expandedUser === user.id" class="user-details">
                    <div class="details-grid">
                        <div class="detail-item">
                            <span class="detail-label">用戶ID:</span>
                            <span class="detail-value">{{ user.id }}</span>
                        </div>
                        <div class="detail-item">
                            <span class="detail-label">註冊時間:</span>
                            <span class="detail-value">{{ formatDate(new Date()) }}</span>
                        </div>
                        <div class="detail-item">
                            <span class="detail-label">最後登錄:</span>
                            <span class="detail-value">{{ getRandomDate() }}</span>
                        </div>
                        <div class="detail-item">
                            <span class="detail-label">狀態:</span>
                            <span class="detail-value" :class="{ active: user.active, inactive: !user.active }">
                                {{ user.active ? '🟢 活躍' : '🔴 停用' }}
                            </span>
                        </div>
                    </div>
                </div>

                <!-- 展開/收起按鈕 -->
                <div class="expand-toggle">
                    <button @click="toggleExpand(user.id)" class="toggle-btn">
                        {{ expandedUser === user.id ? '收起詳情 ▲' : '展開詳情 ▼' }}
                    </button>
                </div>
            </div>
        </div>

        <!-- 空狀態 -->
        <div v-if="filteredUsers.length === 0" class="empty-state">
            <div class="empty-icon">👤</div>
            <div class="empty-text">
                <h5>沒有找到用戶</h5>
                <p>{{ searchQuery || roleFilter ? '請調整搜索條件' : '還沒有任何用戶' }}</p>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

// 定義 Props
const props = defineProps({
    users: {
        type: Array,
        default: () => []
    }
})

// 定義事件發射
const emit = defineEmits(['user-updated', 'user-deleted', 'task-completed'])

// 響應式數據
const searchQuery = ref('')
const roleFilter = ref('')
const editingUser = ref(null)
const expandedUser = ref(null)

// 計算屬性
const filteredUsers = computed(() => {
    let filtered = props.users.filter(user => {
        const matchesSearch = user.name.toLowerCase().includes(searchQuery.value.toLowerCase()) ||
            user.email.toLowerCase().includes(searchQuery.value.toLowerCase())
        const matchesRole = !roleFilter.value || user.role === roleFilter.value
        return matchesSearch && matchesRole
    })

    // 為用戶添加活躍狀態（模擬）
    return filtered.map(user => ({
        ...user,
        active: user.active !== undefined ? user.active : Math.random() > 0.3
    }))
})

const adminCount = computed(() => {
    return props.users.filter(user => user.role === 'admin').length
})

const userCount = computed(() => {
    return props.users.filter(user => user.role === 'user').length
})

// 方法
const editUser = (user) => {
    editingUser.value = { ...user }
}

const saveUser = () => {
    if (editingUser.value) {
        emit('user-updated', editingUser.value)
        emit('task-completed', 'eventEmit')
        editingUser.value = null
    }
}

const cancelEdit = () => {
    editingUser.value = null
}

const deleteUser = (userId) => {
    const user = props.users.find(u => u.id === userId)
    if (user && confirm(`確定要刪除用戶 ${user.name} 嗎？`)) {
        emit('user-deleted', userId)
        emit('task-completed', 'eventEmit')
    }
}

const toggleUserStatus = (user) => {
    const updatedUser = { ...user, active: !user.active }
    emit('user-updated', updatedUser)
    alert(`用戶 ${user.name} 已${updatedUser.active ? '啟用' : '停用'}`)
}

const toggleExpand = (userId) => {
    expandedUser.value = expandedUser.value === userId ? null : userId
}

const formatDate = (date) => {
    return date.toLocaleDateString('zh-TW', {
        year: 'numeric',
        month: 'short',
        day: 'numeric',
        hour: '2-digit',
        minute: '2-digit'
    })
}

const getRandomDate = () => {
    const now = new Date()
    const randomDays = Math.floor(Math.random() * 30)
    const randomDate = new Date(now.getTime() - randomDays * 24 * 60 * 60 * 1000)
    return formatDate(randomDate)
}

// 組件掛載時標記任務完成
onMounted(() => {
    emit('task-completed', 'propsUsage')
    emit('task-completed', 'slotUsage')
})
</script>

<style scoped>
.user-list {
    background: white;
    border-radius: 12px;
    padding: 25px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    border: 1px solid #e9ecef;
}

.list-header {
    margin-bottom: 20px;
    padding-bottom: 15px;
    border-bottom: 2px solid #f1f3f4;
}

.list-header h4 {
    margin: 0 0 10px 0;
    color: #2c3e50;
    font-size: 1.3em;
}

.list-stats {
    display: flex;
    gap: 20px;
    flex-wrap: wrap;
}

.stat-item {
    padding: 6px 12px;
    background: #f8f9fa;
    border-radius: 20px;
    font-size: 0.85em;
    color: #495057;
    border: 1px solid #dee2e6;
}

.list-controls {
    display: flex;
    gap: 15px;
    margin-bottom: 25px;
    align-items: center;
}

.search-box {
    flex: 1;
}

.search-input {
    width: 100%;
    padding: 10px 15px;
    border: 2px solid #dee2e6;
    border-radius: 25px;
    font-size: 14px;
    transition: border-color 0.3s ease;
    box-sizing: border-box;
}

.search-input:focus {
    outline: none;
    border-color: #007bff;
}

.filter-select {
    padding: 10px 15px;
    border: 2px solid #dee2e6;
    border-radius: 8px;
    font-size: 14px;
    background: white;
    cursor: pointer;
}

.user-cards {
    display: grid;
    gap: 20px;
}

.user-card {
    border: 2px solid #e9ecef;
    border-radius: 12px;
    overflow: hidden;
    transition: all 0.3s ease;
    background: white;
}

.user-card:hover {
    border-color: #007bff;
    box-shadow: 0 4px 12px rgba(0, 123, 255, 0.15);
}

.user-card.editing {
    border-color: #ffc107;
    background: #fffbf0;
}

.display-mode {
    padding: 20px;
    display: flex;
    align-items: center;
    gap: 20px;
}

.user-avatar {
    width: 60px;
    height: 60px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2em;
    background: #f8f9fa;
    border-radius: 50%;
    border: 2px solid #dee2e6;
}

.user-info {
    flex: 1;
}

.user-name {
    font-size: 1.1em;
    font-weight: 600;
    color: #2c3e50;
    margin-bottom: 4px;
}

.user-email {
    color: #6c757d;
    font-size: 0.9em;
    margin-bottom: 8px;
}

.user-badge-container {
    margin-bottom: 8px;
}

.default-badge {
    padding: 4px 8px;
    border-radius: 12px;
    font-size: 0.8em;
    font-weight: 600;
}

.default-badge.admin {
    background: #ffd700;
    color: #333;
}

.default-badge.user {
    background: #e3f2fd;
    color: #1976d2;
}

.default-badge.editor {
    background: #e8f5e8;
    color: #2e7d32;
}

.user-bio {
    color: #495057;
    font-size: 0.85em;
    font-style: italic;
    line-height: 1.4;
}

.user-actions {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

.action-btn {
    padding: 8px 12px;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    font-size: 0.8em;
    font-weight: 500;
    transition: all 0.3s ease;
    white-space: nowrap;
}

.edit-btn {
    background: #007bff;
    color: white;
}

.edit-btn:hover {
    background: #0056b3;
}

.delete-btn {
    background: #dc3545;
    color: white;
}

.delete-btn:hover {
    background: #c82333;
}

.status-btn {
    background: #28a745;
    color: white;
}

.status-btn:hover {
    background: #218838;
}

.edit-mode {
    padding: 20px;
    background: #fffbf0;
}

.edit-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20px;
}

.edit-header h5 {
    margin: 0;
    color: #495057;
}

.edit-actions {
    display: flex;
    gap: 10px;
}

.save-btn {
    background: #28a745;
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 6px;
    cursor: pointer;
    font-size: 0.85em;
}

.cancel-btn {
    background: #6c757d;
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 6px;
    cursor: pointer;
    font-size: 0.85em;
}

.edit-form {
    display: grid;
    gap: 15px;
}

.edit-group {
    display: flex;
    align-items: center;
    gap: 10px;
}

.edit-group label {
    min-width: 80px;
    font-weight: 600;
    color: #495057;
}

.edit-input,
.edit-select {
    flex: 1;
    padding: 8px 12px;
    border: 2px solid #dee2e6;
    border-radius: 6px;
    font-size: 14px;
}

.user-details {
    padding: 20px;
    background: #f8f9fa;
    border-top: 1px solid #dee2e6;
}

.details-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 15px;
}

.detail-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px;
    background: white;
    border-radius: 6px;
}

.detail-label {
    font-weight: 600;
    color: #495057;
}

.detail-value {
    color: #6c757d;
}

.detail-value.active {
    color: #28a745;
}

.detail-value.inactive {
    color: #dc3545;
}

.expand-toggle {
    padding: 10px 20px;
    background: #f8f9fa;
    border-top: 1px solid #dee2e6;
    text-align: center;
}

.toggle-btn {
    background: none;
    border: none;
    color: #007bff;
    cursor: pointer;
    font-size: 0.85em;
    padding: 5px 10px;
    border-radius: 4px;
    transition: all 0.3s ease;
}

.toggle-btn:hover {
    background: #e3f2fd;
}

.empty-state {
    text-align: center;
    padding: 60px 20px;
    color: #6c757d;
}

.empty-icon {
    font-size: 4em;
    margin-bottom: 20px;
    opacity: 0.5;
}

.empty-text h5 {
    margin: 0 0 10px 0;
    color: #495057;
}

.empty-text p {
    margin: 0;
    font-size: 0.9em;
}

@media (max-width: 768px) {
    .list-controls {
        flex-direction: column;
        align-items: stretch;
    }

    .display-mode {
        flex-direction: column;
        text-align: center;
        gap: 15px;
    }

    .user-actions {
        flex-direction: row;
        justify-content: center;
    }

    .edit-group {
        flex-direction: column;
        align-items: stretch;
    }

    .edit-group label {
        min-width: auto;
    }

    .details-grid {
        grid-template-columns: 1fr;
    }
}
</style>
