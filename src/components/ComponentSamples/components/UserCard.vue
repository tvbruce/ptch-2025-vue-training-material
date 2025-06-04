<template>
    <div class="user-card">
        <div class="card-header">
            <h4>{{ props.name || '訪客' }}</h4>
            <span v-if="props.isVip" class="vip-badge">VIP</span>
        </div>
        <div class="card-body">
            <p class="user-age">年齡: {{ props.age || '未提供' }}</p>
            <div class="user-status">
                <span :class="['status-badge', props.isVip ? 'vip' : 'regular']">
                    {{ props.isVip ? '尊貴會員' : '一般會員' }}
                </span>
            </div>
        </div>
    </div>
</template>

<script setup>
const props = defineProps({
    name: String,
    age: Number,
    isVip: Boolean
})
</script>
