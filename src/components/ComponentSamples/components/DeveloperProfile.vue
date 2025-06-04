<template>
    <div class="developer-profile">
        <div class="profile-header">
            <h4>{{ props.profile.name }}</h4>
            <div class="location">
                <span class="location-icon">📍</span>
                {{ props.profile.location.city }}, {{ props.profile.location.country }}
            </div>
        </div>
        <div class="profile-body">
            <div class="skills-section">
                <h5>技能清單</h5>
                <div class="skills-list">
                    <span v-for="skill in props.profile.skills" :key="skill" class="skill-tag">
                        {{ skill }}
                    </span>
                </div>
                <p v-if="props.profile.skills.length === 0" class="no-skills">
                    尚未添加技能
                </p>
            </div>
            <div class="profile-stats">
                <div class="stat-item">
                    <span class="stat-label">技能數量</span>
                    <span class="stat-value">{{ props.profile.skills.length }}</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">經驗等級</span>
                    <span class="stat-value">{{ getExperienceLevel() }}</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
const props = defineProps({
    profile: {
        type: Object,
        default: () => ({
            name: '開發者',
            skills: [],
            location: { city: '台北', country: '台灣' }
        }),
        validator: (value) => {
            return value && typeof value === 'object' &&
                Array.isArray(value.skills)
        }
    }
})

const getExperienceLevel = () => {
    const skillCount = props.profile.skills.length
    if (skillCount === 0) return '新手'
    if (skillCount <= 2) return '初級'
    if (skillCount <= 4) return '中級'
    if (skillCount <= 6) return '高級'
    return '專家'
}
</script>
