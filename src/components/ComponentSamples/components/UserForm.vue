<template>
    <div class="user-form">
        <div class="form-header">
            <h4>👤 添加新用戶</h4>
            <p>填寫用戶基本信息</p>
        </div>

        <form @submit.prevent="addUser" class="form-container">
            <div class="form-group">
                <label for="name">姓名 *</label>
                <input id="name" v-model="userForm.name" type="text" placeholder="請輸入姓名" required class="form-input"
                    :class="{ error: errors.name }" />
                <span v-if="errors.name" class="error-message">{{ errors.name }}</span>
            </div>

            <div class="form-group">
                <label for="email">電子郵件 *</label>
                <input id="email" v-model="userForm.email" type="email" placeholder="請輸入電子郵件" required
                    class="form-input" :class="{ error: errors.email }" />
                <span v-if="errors.email" class="error-message">{{ errors.email }}</span>
            </div>

            <div class="form-group">
                <label for="role">角色 *</label>
                <select id="role" v-model="userForm.role" required class="form-select">
                    <option value="">請選擇角色</option>
                    <option value="admin">管理員</option>
                    <option value="user">一般用戶</option>
                    <option value="editor">編輯者</option>
                </select>
            </div>

            <div class="form-group">
                <label for="avatar">頭像</label>
                <div class="avatar-selector">
                    <div v-for="avatar in avatarOptions" :key="avatar" class="avatar-option"
                        :class="{ selected: userForm.avatar === avatar }" @click="userForm.avatar = avatar">
                        {{ avatar }}
                    </div>
                </div>
            </div>

            <div class="form-group">
                <label for="bio">個人簡介</label>
                <textarea id="bio" v-model="userForm.bio" placeholder="請輸入個人簡介（選填）" class="form-textarea"
                    rows="3"></textarea>
                <div class="char-count">{{ bioLength }}/200 字</div>
            </div>

            <div class="form-actions">
                <button type="submit" class="submit-btn" :disabled="!isFormValid">
                    ✅ 添加用戶
                </button>
                <button type="button" @click="resetForm" class="reset-btn">
                    🔄 重置
                </button>
            </div>
        </form>

        <!-- 表單預覽 -->
        <div v-if="isFormValid" class="form-preview">
            <h5>👀 預覽</h5>
            <div class="preview-card">
                <div class="preview-avatar">{{ userForm.avatar }}</div>
                <div class="preview-content">
                    <div class="preview-name">{{ userForm.name }}</div>
                    <div class="preview-email">{{ userForm.email }}</div>
                    <div class="preview-role" :class="userForm.role">
                        {{ getRoleText(userForm.role) }}
                    </div>
                    <div v-if="userForm.bio" class="preview-bio">{{ userForm.bio }}</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

// 定義事件發射
const emit = defineEmits(['user-added', 'task-completed'])

// 表單數據
const userForm = ref({
    name: '',
    email: '',
    role: '',
    avatar: '👤',
    bio: ''
})

// 錯誤信息
const errors = ref({
    name: '',
    email: ''
})

// 頭像選項
const avatarOptions = ['👤', '👨‍💼', '👩‍💻', '👨‍🎓', '👩‍🎓', '👨‍🔬', '👩‍🔬', '👨‍🎨', '👩‍🎨']

// 計算屬性
const bioLength = computed(() => {
    return userForm.value.bio.length
})

const isFormValid = computed(() => {
    return userForm.value.name.trim() !== '' &&
        userForm.value.email.trim() !== '' &&
        userForm.value.role !== '' &&
        !errors.value.name &&
        !errors.value.email
})

// 方法
const validateName = () => {
    if (userForm.value.name.trim().length < 2) {
        errors.value.name = '姓名至少需要2個字符'
    } else {
        errors.value.name = ''
    }
}

const validateEmail = () => {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
    if (!emailRegex.test(userForm.value.email)) {
        errors.value.email = '請輸入有效的電子郵件地址'
    } else {
        errors.value.email = ''
    }
}

const getRoleText = (role) => {
    const roleMap = {
        admin: '👑 管理員',
        user: '👤 一般用戶',
        editor: '✏️ 編輯者'
    }
    return roleMap[role] || role
}

const addUser = () => {
    validateName()
    validateEmail()

    if (!isFormValid.value) return

    const newUser = {
        name: userForm.value.name.trim(),
        email: userForm.value.email.trim(),
        role: userForm.value.role,
        avatar: userForm.value.avatar,
        bio: userForm.value.bio.trim()
    }

    // 發射事件到父組件
    emit('user-added', newUser)
    emit('task-completed', 'eventEmit')

    // 重置表單
    resetForm()

    // 顯示成功消息
    alert(`用戶 ${newUser.name} 添加成功！`)
}

const resetForm = () => {
    userForm.value = {
        name: '',
        email: '',
        role: '',
        avatar: '👤',
        bio: ''
    }
    errors.value = {
        name: '',
        email: ''
    }
}

// 組件掛載時標記任務完成
onMounted(() => {
    emit('task-completed', 'propsUsage')
})
</script>

<style scoped>
.user-form {
    background: white;
    border-radius: 12px;
    padding: 25px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    border: 1px solid #e9ecef;
}

.form-header {
    text-align: center;
    margin-bottom: 25px;
    padding-bottom: 15px;
    border-bottom: 2px solid #f1f3f4;
}

.form-header h4 {
    margin: 0 0 8px 0;
    color: #2c3e50;
    font-size: 1.3em;
}

.form-header p {
    margin: 0;
    color: #6c757d;
    font-size: 0.9em;
}

.form-container {
    margin-bottom: 25px;
}

.form-group {
    margin-bottom: 20px;
}

.form-group label {
    display: block;
    margin-bottom: 8px;
    font-weight: 600;
    color: #495057;
}

.form-input,
.form-select,
.form-textarea {
    width: 100%;
    padding: 12px 16px;
    border: 2px solid #dee2e6;
    border-radius: 8px;
    font-size: 14px;
    transition: border-color 0.3s ease;
    box-sizing: border-box;
}

.form-input:focus,
.form-select:focus,
.form-textarea:focus {
    outline: none;
    border-color: #007bff;
    box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.1);
}

.form-input.error,
.form-select.error {
    border-color: #dc3545;
}

.error-message {
    display: block;
    color: #dc3545;
    font-size: 0.8em;
    margin-top: 5px;
}

.form-textarea {
    resize: vertical;
    min-height: 80px;
    font-family: inherit;
}

.char-count {
    text-align: right;
    font-size: 0.8em;
    color: #6c757d;
    margin-top: 5px;
}

.avatar-selector {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(50px, 1fr));
    gap: 10px;
    margin-top: 8px;
}

.avatar-option {
    width: 50px;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.5em;
    border: 2px solid #dee2e6;
    border-radius: 50%;
    cursor: pointer;
    transition: all 0.3s ease;
    background: #f8f9fa;
}

.avatar-option:hover {
    border-color: #007bff;
    background: #e3f2fd;
    transform: scale(1.1);
}

.avatar-option.selected {
    border-color: #007bff;
    background: #007bff;
    color: white;
    transform: scale(1.1);
}

.form-actions {
    display: flex;
    gap: 15px;
    justify-content: center;
    margin-top: 25px;
}

.submit-btn,
.reset-btn {
    padding: 12px 24px;
    border: none;
    border-radius: 8px;
    font-size: 14px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
}

.submit-btn {
    background: #28a745;
    color: white;
}

.submit-btn:hover:not(:disabled) {
    background: #218838;
    transform: translateY(-2px);
}

.submit-btn:disabled {
    background: #6c757d;
    cursor: not-allowed;
    transform: none;
}

.reset-btn {
    background: #6c757d;
    color: white;
}

.reset-btn:hover {
    background: #5a6268;
    transform: translateY(-2px);
}

.form-preview {
    background: #f8f9fa;
    border-radius: 10px;
    padding: 20px;
    border: 1px solid #dee2e6;
}

.form-preview h5 {
    margin: 0 0 15px 0;
    color: #495057;
    font-size: 1.1em;
}

.preview-card {
    background: white;
    border-radius: 8px;
    padding: 15px;
    display: flex;
    align-items: center;
    gap: 15px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.preview-avatar {
    width: 60px;
    height: 60px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2em;
    background: #e3f2fd;
    border-radius: 50%;
    border: 2px solid #007bff;
}

.preview-content {
    flex: 1;
}

.preview-name {
    font-size: 1.1em;
    font-weight: 600;
    color: #2c3e50;
    margin-bottom: 4px;
}

.preview-email {
    color: #6c757d;
    font-size: 0.9em;
    margin-bottom: 6px;
}

.preview-role {
    display: inline-block;
    padding: 4px 8px;
    border-radius: 12px;
    font-size: 0.8em;
    font-weight: 600;
    margin-bottom: 8px;
}

.preview-role.admin {
    background: #ffd700;
    color: #333;
}

.preview-role.user {
    background: #e3f2fd;
    color: #1976d2;
}

.preview-role.editor {
    background: #e8f5e8;
    color: #2e7d32;
}

.preview-bio {
    color: #495057;
    font-size: 0.85em;
    line-height: 1.4;
    font-style: italic;
}

@media (max-width: 768px) {
    .form-actions {
        flex-direction: column;
    }

    .preview-card {
        flex-direction: column;
        text-align: center;
    }

    .avatar-selector {
        grid-template-columns: repeat(5, 1fr);
    }
}
</style>
