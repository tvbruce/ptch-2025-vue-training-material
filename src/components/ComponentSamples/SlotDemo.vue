<template>
    <div class="slot-demo">
        <h2>Slot 插槽系統</h2>
        <p class="route-info">📍 路徑：/ComponentSamples/SlotDemo.vue</p>

        <!-- 默認插槽 -->
        <div class="demo-section">
            <h3>1. 默認插槽 (Default Slot)</h3>
            <div class="result">
                <BasicCard>
                    <h4>這是通過插槽插入的標題</h4>
                    <p>這段內容會顯示在卡片內部，展示了默認插槽的基本用法。</p>
                    <button class="btn btn-primary">插槽中的按鈕</button>
                </BasicCard>

                <BasicCard>
                    <div class="custom-content">
                        <span class="icon">🎉</span>
                        <strong>完全自定義的內容!</strong>
                    </div>
                </BasicCard>
            </div>
            <div class="code-example">
                <pre v-pre><code>// BasicCard.vue - 子組件
&lt;template&gt;
  &lt;div class="card"&gt;
    &lt;div class="card-header"&gt;卡片標題&lt;/div&gt;
    &lt;div class="card-body"&gt;
      &lt;slot&gt;&lt;/slot&gt;  &lt;!-- 默認插槽 --&gt;
    &lt;/div&gt;
  &lt;/div&gt;
&lt;/template&gt;

// 使用方式
&lt;BasicCard&gt;
  &lt;h4&gt;插槽內容&lt;/h4&gt;
  &lt;p&gt;任何HTML內容都可以放在這裡&lt;/p&gt;
&lt;/BasicCard&gt;</code></pre>
            </div>
        </div>

        <!-- 具名插槽 -->
        <div class="demo-section">
            <h3>2. 具名插槽 (Named Slots)</h3>
            <div class="result">
                <LayoutCard>
                    <template #header>
                        <h4>自定義標題區域</h4>
                        <span class="badge">New</span>
                    </template>

                    <template #default>
                        <p>這是主要內容區域，使用默認插槽。</p>
                        <p>可以包含任何複雜的內容結構。</p>
                    </template>

                    <template #footer>
                        <button class="btn btn-primary">確認</button>
                        <button class="btn btn-secondary">取消</button>
                    </template>
                </LayoutCard>
            </div>
            <div class="code-example">
                <pre v-pre><code>// LayoutCard.vue - 具名插槽
            &lt;template&gt;
            &lt;div class="layout-card"&gt;
            &lt;header class="card-header"&gt;
            &lt;slot name="header"&gt;默認標題&lt;/slot&gt;
            &lt;/header&gt;
            &lt;main class="card-body"&gt;
            &lt;slot&gt;&lt;/slot&gt; &lt;!-- 默認插槽 --&gt;
            &lt;/main&gt;
            &lt;footer class="card-footer"&gt;
            &lt;slot name="footer"&gt;默認底部&lt;/slot&gt;
            &lt;/footer&gt;
            &lt;/div&gt;
            &lt;/template&gt;

            // 使用方式
            &lt;LayoutCard&gt;
            &lt;template #header&gt;自定義標題&lt;/template&gt;
            &lt;template #default&gt;主要內容&lt;/template&gt;
            &lt;template #footer&gt;自定義底部&lt;/template&gt;
            &lt;/LayoutCard&gt;</code></pre>
            </div>
        </div>

        <!-- 作用域插槽 -->
        <div class="demo-section">
            <h3>3. 作用域插槽 (Scoped Slots)</h3>
            <div class="controls">
                <button @click="addUser" class="btn btn-primary">新增用戶</button>
                <button @click="shuffleUsers" class="btn btn-secondary">打亂順序</button>
            </div>
            <div class="result">
                <UserList :users="users">
                    <template #user="{ user, index }">
                        <div class="custom-user-item">
                            <div class="user-avatar">{{ user.name.charAt(0) }}</div>
                            <div class="user-info">
                                <h5>{{ user.name }}</h5>
                                <p>{{ user.role }} - {{ user.department }}</p>
                                <small>編號: #{{ index + 1 }}</small>
                            </div>
                            <div class="user-actions">
                                <button @click="promoteUser(user)" class="btn btn-small btn-success">
                                    升職
                                </button>
                            </div>
                        </div>
                    </template>
                </UserList>
            </div>
            <div class="code-example">
                <pre v-pre><code>// UserList.vue - 作用域插槽
                &lt;template&gt;
                &lt;div class="user-list"&gt;
                &lt;div v-for="(user, index) in users" :key="user.id"&gt;
                &lt;slot name="user" :user="user" :index="index"&gt;
                &lt;!-- 默認顯示方式 --&gt;
                &lt;div&gt;{{ user.name }} - {{ user.role }}&lt;/div&gt;
                &lt;/slot&gt;
                &lt;/div&gt;
                &lt;/div&gt;
                &lt;/template&gt;

                // 使用方式 - 可以訪問子組件的數據
                &lt;UserList :users="users"&gt;
                &lt;template #user="{ user, index }"&gt;
                &lt;div&gt;自定義顯示: {{ user.name }} (#{{ index }}))&lt;/div&gt;
                &lt;/template&gt;
                &lt;/UserList&gt;</code></pre>
            </div>
        </div>

        <!-- 動態插槽名 -->
        <div class="demo-section">
            <h3>4. 動態插槽名與插槽後備內容</h3>
            <div class="controls">
                <select v-model="selectedSlot" class="select-field">
                    <option value="header">頭部插槽</option>
                    <option value="content">內容插槽</option>
                    <option value="sidebar">側邊欄插槽</option>
                </select>
            </div>
            <div class="result">
                <FlexibleLayout>
                    <template #[selectedSlot]>
                        <div class="dynamic-content">
                            <h5>動態插槽內容</h5>
                            <p>當前激活的插槽: <strong>{{ selectedSlot }}</strong></p>
                            <p>這個內容會根據選擇的插槽位置動態顯示。</p>
                        </div>
                    </template>
                </FlexibleLayout>
            </div>
            <div class="code-example">
                <pre v-pre><code>// FlexibleLayout.vue - 帶後備內容的插槽
                &lt;template&gt;
                &lt;div class="flexible-layout"&gt;
                &lt;div class="layout-header"&gt;
                &lt;slot name="header"&gt;
                &lt;h4&gt;默認標題&lt;/h4&gt;
                &lt;/slot&gt;
                &lt;/div&gt;
                &lt;div class="layout-main"&gt;
                &lt;div class="layout-content"&gt;
                &lt;slot name="content"&gt;
                &lt;p&gt;默認內容區域&lt;/p&gt;
                &lt;/slot&gt;
                &lt;/div&gt;
                &lt;div class="layout-sidebar"&gt;
                &lt;slot name="sidebar"&gt;
                &lt;p&gt;默認側邊欄&lt;/p&gt;
                &lt;/slot&gt;
                &lt;/div&gt;
                &lt;/div&gt;
                &lt;/div&gt;
                &lt;/template&gt;

                // 動態插槽名使用
                &lt;FlexibleLayout&gt;
                &lt;template #[dynamicSlotName]&gt;
                動態內容
                &lt;/template&gt;
                &lt;/FlexibleLayout&gt;</code></pre>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
import BasicCard from './components/BasicCard.vue'
import LayoutCard from './components/LayoutCard.vue'
import UserList from './components/UserList.vue'
import FlexibleLayout from './components/FlexibleLayout.vue'

// 作用域插槽數據
const users = ref([
    { id: 1, name: '張小明', role: '前端工程師', department: '技術部' },
    { id: 2, name: '李小華', role: '後端工程師', department: '技術部' },
    { id: 3, name: '王小美', role: '設計師', department: '設計部' },
    { id: 4, name: '陳小強', role: '產品經理', department: '產品部' }
])

// 動態插槽
const selectedSlot = ref('header')

// 方法
const addUser = () => {
    const newId = Math.max(...users.value.map(u => u.id)) + 1
    const names = ['趙小紅', '劉小青', '蔡小藍', '林小綠']
    const roles = ['工程師', '設計師', '產品經理', '測試工程師']
    const departments = ['技術部', '設計部', '產品部', '測試部']

    users.value.push({
        id: newId,
        name: names[Math.floor(Math.random() * names.length)],
        role: roles[Math.floor(Math.random() * roles.length)],
        department: departments[Math.floor(Math.random() * departments.length)]
    })
}

const shuffleUsers = () => {
    users.value = users.value.sort(() => Math.random() - 0.5)
}

const promoteUser = (user) => {
    const promotions = {
        '工程師': '資深工程師',
        '前端工程師': '資深前端工程師',
        '後端工程師': '資深後端工程師',
        '設計師': '資深設計師',
        '產品經理': '資深產品經理'
    }

    if (promotions[user.role]) {
        user.role = promotions[user.role]
    }
}
</script>
