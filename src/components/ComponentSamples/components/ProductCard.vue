<template>
    <div class="product-card">
        <div class="product-header">
            <h4>{{ props.name }}</h4>
            <span class="category-badge" :class="props.category">
                {{ getCategoryText(props.category) }}
            </span>
        </div>
        <div class="product-body">
            <div class="price-section">
                <span class="price">NT$ {{ formatPrice(props.price) }}</span>
                <span v-if="props.price === 0" class="free-badge">免費</span>
            </div>
            <div class="product-info">
                <p>分類: {{ getCategoryText(props.category) }}</p>
                <p>價格區間: {{ getPriceRange(props.price) }}</p>
            </div>
        </div>
    </div>
</template>

<script setup>
const props = defineProps({
    name: {
        type: String,
        default: '未命名產品'
    },
    price: {
        type: Number,
        default: 0,
        validator: (value) => value >= 0
    },
    category: {
        type: String,
        default: 'general',
        validator: (value) =>
            ['electronics', 'clothing', 'books', 'general'].includes(value)
    }
})

const getCategoryText = (category) => {
    const categoryMap = {
        electronics: '電子產品',
        clothing: '服飾',
        books: '書籍',
        general: '一般商品'
    }
    return categoryMap[category] || '一般商品'
}

const formatPrice = (price) => {
    return price.toLocaleString()
}

const getPriceRange = (price) => {
    if (price === 0) return '免費'
    if (price < 1000) return '經濟實惠'
    if (price < 10000) return '中等價位'
    if (price < 50000) return '高階商品'
    return '奢華商品'
}
</script>
