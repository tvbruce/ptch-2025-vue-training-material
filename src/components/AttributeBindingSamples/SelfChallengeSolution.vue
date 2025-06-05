<template>
    <div class="solution">
        <h2>✅ 解答 - 屬性綁定</h2>
        <p>完整實現動態卡片組件，展示各種屬性綁定技巧</p>

        <!-- 基本屬性綁定 -->
        <div class="demo-card">
            <h4>基本屬性綁定</h4>
            <img :src="cardImageSrc" :alt="`${selectedTheme} 主題圖片`" />
            <a v-bind="linkAttributes">{{ linkTitle || '示例連結' }}</a>
        </div>

        <!-- 動態 Class 綁定 -->
        <div class="demo-card">
            <h4>動態 Class 綁定</h4>
            <div :class="cardClasses" class="dynamic-card">
                <p>CSS 類別會根據狀態動態變化</p>
            </div>
        </div>

        <!-- 動態 Style 綁定 -->
        <div class="demo-card">
            <h4>動態 Style 綁定</h4>
            <div :style="cardStyles" class="styled-card">
                <p>內聯樣式動態變化</p>
            </div>
        </div>

        <!-- 控制面板 -->
        <div class="controls">
            <select v-model="selectedTheme">
                <option value="nature">自然</option>
                <option value="technology">科技</option>
                <option value="art">藝術</option>
            </select>

            <label><input type="checkbox" v-model="isActive" /> 激活</label>
            <label><input type="checkbox" v-model="isHighlighted" /> 高亮</label>
            <label><input type="checkbox" v-model="isLoading" /> 載入中</label>

            <input type="color" v-model="customColor" />
            <input type="range" v-model="borderWidth" min="0" max="10" />
            <input type="range" v-model="opacity" min="0" max="100" />
            <input type="range" v-model="scale" min="0.5" max="2" step="0.1" />

            <input v-model="linkUrl" placeholder="連結網址" />
            <input v-model="linkTitle" placeholder="連結標題" />
            <label><input type="checkbox" v-model="openInNewTab" /> 新分頁</label>

            <button @click="resetCardSettings">重置</button>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const selectedTheme = ref('nature')
const isActive = ref(false)
const isHighlighted = ref(false)
const isLoading = ref(false)
const customColor = ref('#ffffff')
const borderWidth = ref(2)
const opacity = ref(100)
const scale = ref(1)
const linkUrl = ref('')
const linkTitle = ref('')
const openInNewTab = ref(false)

const cardImageSrc = computed(() => {
    const themeMap = {
        'nature': '/images/nature.jpg',
        'technology': '/images/tech.jpg',
        'art': '/images/art.jpg'
    }
    return themeMap[selectedTheme.value] || '/images/default.jpg'
})

const cardClasses = computed(() => {
    return {
        'dynamic-card': true,
        [`theme-${selectedTheme.value}`]: true,
        'active': isActive.value,
        'highlighted': isHighlighted.value,
        'loading': isLoading.value
    }
})

const cardStyles = computed(() => {
    return {
        backgroundColor: customColor.value,
        borderWidth: `${borderWidth.value}px`,
        opacity: opacity.value / 100,
        transform: `scale(${scale.value})`
    }
})

const linkAttributes = computed(() => {
    const attrs = {
        href: linkUrl.value || '#',
        title: linkTitle.value
    }

    if (openInNewTab.value) {
        attrs.target = '_blank'
        attrs.rel = 'noopener noreferrer'
    } else {
        attrs.target = '_self'
    }

    Object.keys(attrs).forEach(key => {
        if (attrs[key] === undefined || attrs[key] === '') {
            delete attrs[key]
        }
    })

    return attrs
})

const resetCardSettings = () => {
    selectedTheme.value = 'nature'
    isActive.value = false
    isHighlighted.value = false
    isLoading.value = false
    customColor.value = '#ffffff'
    borderWidth.value = 2
    opacity.value = 100
    scale.value = 1
    linkUrl.value = ''
    linkTitle.value = ''
    openInNewTab.value = false
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

.dynamic-card {
    padding: 20px;
    border: 2px solid #dee2e6;
    border-radius: 10px;
    transition: all 0.3s ease;
}

.dynamic-card.active {
    border-color: #28a745;
    background: #f8fff9;
}

.dynamic-card.highlighted {
    box-shadow: 0 0 20px rgba(255, 193, 7, 0.5);
}

.theme-nature {
    background: linear-gradient(135deg, #e8f5e8 0%, #c8e6c9 100%);
}

.theme-technology {
    background: linear-gradient(135deg, #e3f2fd 0%, #bbdefb 100%);
}

.theme-art {
    background: linear-gradient(135deg, #fce4ec 0%, #f8bbd9 100%);
}

.styled-card {
    padding: 20px;
    border: 2px solid #ccc;
    border-radius: 10px;
    transition: all 0.3s ease;
}

.controls {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    align-items: center;
    padding: 20px;
    background: #f8f9fa;
    border-radius: 10px;
}

.controls input,
.controls select,
.controls button {
    padding: 8px 12px;
    border: 1px solid #ced4da;
    border-radius: 5px;
}

.controls button {
    background: #dc3545;
    color: white;
    border: none;
    cursor: pointer;
}
</style>
