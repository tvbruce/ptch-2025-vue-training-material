<template>
    <div class="settings-tab">
        <h4>系統設定</h4>
        <div class="settings-content">
            <div class="setting-group">
                <label>主題設定:</label>
                <select v-model="currentTheme" @change="changeTheme" class="select-field">
                    <option value="light">淺色主題</option>
                    <option value="dark">深色主題</option>
                    <option value="auto">自動</option>
                </select>
            </div>

            <div class="setting-group">
                <label>語言設定:</label>
                <select v-model="currentLanguage" @change="changeLanguage" class="select-field">
                    <option value="zh-TW">繁體中文</option>
                    <option value="zh-CN">簡體中文</option>
                    <option value="en">English</option>
                </select>
            </div>

            <div class="setting-group">
                <label>
                    <input type="checkbox" v-model="notifications" @change="toggleNotifications">
                    啟用通知
                </label>
            </div>

            <div class="setting-group">
                <label>
                    <input type="checkbox" v-model="autoSave" @change="toggleAutoSave">
                    自動儲存
                </label>
            </div>

            <div class="current-settings">
                <h5>目前設定:</h5>
                <p>主題: {{ getThemeText(currentTheme) }}</p>
                <p>語言: {{ getLanguageText(currentLanguage) }}</p>
                <p>通知: {{ notifications ? '已啟用' : '已停用' }}</p>
                <p>自動儲存: {{ autoSave ? '已啟用' : '已停用' }}</p>
            </div>

            <div class="action-buttons">
                <button @click="resetSettings" class="btn btn-warning">重置設定</button>
                <button @click="saveSettings" class="btn btn-success">儲存設定</button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
    tabData: {
        type: Object,
        default: () => ({})
    }
})

const currentTheme = ref(props.tabData.theme || 'light')
const currentLanguage = ref(props.tabData.language || 'zh-TW')
const notifications = ref(true)
const autoSave = ref(false)

const changeTheme = () => {
    console.log('主題變更為:', currentTheme.value)
}

const changeLanguage = () => {
    console.log('語言變更為:', currentLanguage.value)
}

const toggleNotifications = () => {
    console.log('通知設定:', notifications.value)
}

const toggleAutoSave = () => {
    console.log('自動儲存設定:', autoSave.value)
}

const getThemeText = (theme) => {
    const themeMap = {
        light: '淺色主題',
        dark: '深色主題',
        auto: '自動'
    }
    return themeMap[theme] || '未知'
}

const getLanguageText = (lang) => {
    const langMap = {
        'zh-TW': '繁體中文',
        'zh-CN': '簡體中文',
        'en': 'English'
    }
    return langMap[lang] || '未知'
}

const resetSettings = () => {
    currentTheme.value = 'light'
    currentLanguage.value = 'zh-TW'
    notifications.value = true
    autoSave.value = false
    alert('設定已重置')
}

const saveSettings = () => {
    alert('設定已儲存')
}
</script>
