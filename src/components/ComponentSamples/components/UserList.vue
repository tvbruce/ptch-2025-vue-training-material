<template>
    <div class="user-list">
        <div v-for="(user, index) in users" :key="user.id" class="user-item">
            <slot name="user" :user="user" :index="index">
                <!-- 默認顯示方式 -->
                <div class="default-user-item">
                    <strong>{{ user.name }}</strong>
                    <span> - {{ user.role }}</span>
                    <small> ({{ user.department }})</small>
                </div>
            </slot>
        </div>
        <div v-if="users.length === 0" class="empty-state">
            沒有用戶數據
        </div>
    </div>
</template>

<script setup>
defineProps({
    users: {
        type: Array,
        default: () => []
    }
})
</script>
