<template>
    <div class="layout-card">
        <header class="card-header">
            <slot name="header">
                <h5>默認標題</h5>
            </slot>
        </header>
        <main class="card-body">
            <slot></slot> <!-- 默認插槽 -->
        </main>
        <footer class="card-footer">
            <slot name="footer">
                <p>默認底部內容</p>
            </slot>
        </footer>
    </div>
</template>

<script setup>
// 具名插槽展示組件
</script>
