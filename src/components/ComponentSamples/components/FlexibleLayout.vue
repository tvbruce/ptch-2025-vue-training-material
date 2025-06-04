<template>
    <div class="flexible-layout">
        <div class="layout-header">
            <slot name="header">
                <h4>默認標題</h4>
                <p>這是頭部的默認內容</p>
            </slot>
        </div>
        <div class="layout-main">
            <div class="layout-content">
                <slot name="content">
                    <div class="default-content">
                        <h5>默認內容區域</h5>
                        <p>當沒有提供 content 插槽時顯示這個默認內容。</p>
                        <ul>
                            <li>這是一個列表項目</li>
                            <li>展示默認內容的樣式</li>
                        </ul>
                    </div>
                </slot>
            </div>
            <div class="layout-sidebar">
                <slot name="sidebar">
                    <div class="default-sidebar">
                        <h6>默認側邊欄</h6>
                        <nav>
                            <ul>
                                <li><a href="#">導航項目 1</a></li>
                                <li><a href="#">導航項目 2</a></li>
                                <li><a href="#">導航項目 3</a></li>
                            </ul>
                        </nav>
                    </div>
                </slot>
            </div>
        </div>
    </div>
</template>

<script setup>
// 展示動態插槽名稱和後備內容的組件
</script>
