<template>
    <div class="basic-card">
        <div class="card-header">
            <h5>基本卡片</h5>
        </div>
        <div class="card-body">
            <slot></slot> <!-- 默認插槽 -->
        </div>
    </div>
</template>

<script setup>
// 無需 props 或其他邏輯，純粹的插槽展示
</script>
