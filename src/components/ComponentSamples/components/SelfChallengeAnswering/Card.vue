<template>
    <div class="card">
        <!-- 🎯 任務：實作卡片標題區域 -->
        <div class="card-header">
            <h4 class="card-title">卡片標題待實作</h4>
        </div>

        <!-- 🎯 任務：實作卡片主要內容區域 -->
        <div class="card-body">
            <p>這是預設內容，請使用插槽自定義內容</p>
        </div>

        <!-- 🎯 任務：實作卡片底部區域 -->
        <div class="card-footer">
            卡片底部內容待實作
        </div>

        <!-- 開發提示區域 -->
        <div class="dev-hints">
            <h6>💡 實作提示：</h6>
            <ul>
                <li>定義 title 和 color props</li>
                <li>使用 雙大括號title雙大括號 顯示標題</li>
                <li>使用 :class="[`card-${color}`]" 設定顏色樣式</li>
                <li>使用 &lt;slot name="header"&gt; 實作 header 插槽</li>
                <li>使用 &lt;slot&gt; 實作預設插槽</li>
                <li>使用 &lt;slot name="footer"&gt; 實作 footer 插槽</li>
                <li>使用 v-if="$slots.header" 條件顯示</li>
            </ul>
        </div>
    </div>
</template>

<script setup>
// 🎯 任務：定義 props
// 提示：定義 title 和 color 屬性
// const props = defineProps({
//   title: {
//     type: String,
//     default: ''
//   },
//   color: {
//     type: String,
//     default: 'default'
//   }
// })
</script>

<style scoped>
.card {
    background: white;
    border-radius: 8px;
    overflow: hidden;
    border: 1px solid #e9ecef;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 1rem;
}

.card-header {
    padding: 1.5rem 1.5rem 0 1.5rem;
    background: #f8f9fa;
}

.card-title {
    margin: 0 0 1rem 0;
    color: #495057;
    font-size: 1.2rem;
}

.card-body {
    padding: 1.5rem;
}

.card-footer {
    padding: 1rem 1.5rem;
    background: #f8f9fa;
    border-top: 1px solid #e9ecef;
    color: #6c757d;
}

.dev-hints {
    background: #fff3cd;
    border-top: 1px solid #ffeaa7;
    padding: 1rem 1.5rem;
    margin: 0;
}

.dev-hints h6 {
    margin: 0 0 0.5rem 0;
    color: #856404;
    font-size: 0.9rem;
}

.dev-hints ul {
    margin: 0;
    padding-left: 1.2rem;
}

.dev-hints li {
    color: #856404;
    font-size: 0.8rem;
    margin-bottom: 0.25rem;
}

/* 顏色主題（學員需要實作的樣式） */
.card-default {
    border-color: #e9ecef;
}

.card-primary {
    border-color: #007bff;
}

.card-primary .card-header {
    background: #007bff;
    color: white;
}

.card-primary .card-title {
    color: white;
}

.card-success {
    border-color: #28a745;
}

.card-success .card-header {
    background: #28a745;
    color: white;
}

.card-success .card-title {
    color: white;
}

@media (max-width: 768px) {

    .card-header,
    .card-body,
    .card-footer,
    .dev-hints {
        padding: 1rem;
    }
}
</style>
