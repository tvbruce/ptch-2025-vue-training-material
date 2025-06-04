<template>
  <div class="profile-tab">
    <h4>個人資料</h4>
    <div class="profile-content">
      <div class="user-profile">
        <div class="avatar">{{ tabData.user?.name?.charAt(0) || 'U' }}</div>
        <div class="user-details">
          <h5>{{ tabData.user?.name || '用戶名' }}</h5>
          <p>{{ tabData.user?.email || 'user@example.com' }}</p>
          <p>最後登入: {{ lastLoginTime }}</p>
        </div>
      </div>

      <div class="profile-stats">
        <div class="stat-item">
          <span class="stat-value">{{ profileViews }}</span>
          <span class="stat-label">檔案查看</span>
        </div>
        <div class="stat-item">
          <span class="stat-value">{{ editCount }}</span>
          <span class="stat-label">編輯次數</span>
        </div>
      </div>

      <div class="action-buttons">
        <button @click="editProfile" class="btn btn-primary">編輯資料</button>
        <button @click="refreshData" class="btn btn-secondary">重新整理</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

defineProps({
  tabData: {
    type: Object,
    default: () => ({})
  }
})

const lastLoginTime = ref(new Date().toLocaleString())
const profileViews = ref(42)
const editCount = ref(3)

const editProfile = () => {
  editCount.value++
  alert('編輯資料功能')
}

const refreshData = () => {
  profileViews.value++
  lastLoginTime.value = new Date().toLocaleString()
}

onMounted(() => {
  profileViews.value++
})
</script>
