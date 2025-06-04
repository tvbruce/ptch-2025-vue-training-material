<template>
  <div class="component-practice">
    <div class="practice-header">
      <h1>🧩 Component 組件化練習</h1>
      <p>學習Vue組件化開發的核心概念</p>
    </div>

    <!-- 練習任務列表 -->
    <div class="task-section">
      <h2>📋 練習任務</h2>
      <div class="task-list">
        <div class="task-item" :class="{ completed: tasks.propsUsage }">
          <span>✅ 使用 Props 傳遞數據給子組件</span>
        </div>
        <div class="task-item" :class="{ completed: tasks.eventEmit }">
          <span>✅ 使用 $emit 從子組件向父組件發送事件</span>
        </div>
        <div class="task-item" :class="{ completed: tasks.slotUsage }">
          <span>✅ 使用插槽(Slot)實現內容分發</span>
        </div>
        <div class="task-item" :class="{ completed: tasks.componentComposition }">
          <span>✅ 組合多個組件構建複雜功能</span>
        </div>
      </div>
    </div>

    <!-- 博客系統練習 -->
    <div class="practice-section">
      <h2>📝 博客系統練習</h2>

      <!-- 文章編輯器 -->
      <div class="editor-section">
        <h3>文章編輯器</h3>
        <ArticleEditor @article-created="handleArticleCreated" @task-completed="updateTask" />
      </div>

      <!-- 文章列表 -->
      <div class="articles-section">
        <h3>文章列表 ({{ articles.length }} 篇文章)</h3>
        <div class="articles-grid">
          <ArticleCard v-for="article in articles" :key="article.id" :article="article" @like="handleLike"
            @delete="handleDelete" @task-completed="updateTask">
            <!-- 使用插槽自定義文章操作 -->
            <template #actions>
              <button class="action-btn share-btn" @click="shareArticle(article)">
                📤 分享
              </button>
            </template>
          </ArticleCard>
        </div>
      </div>

      <!-- 統計面板 -->
      <div class="stats-section">
        <h3>統計面板</h3>
        <StatsPanel :total-articles="articles.length" :total-likes="totalLikes" :most-liked-article="mostLikedArticle"
          @task-completed="updateTask" />
      </div>
    </div>

    <!-- 用戶管理練習 -->
    <div class="practice-section">
      <h2>👥 用戶管理練習</h2>

      <div class="user-management">
        <UserForm @user-added="handleUserAdded" @task-completed="updateTask" />

        <UserList :users="users" @user-updated="handleUserUpdated" @user-deleted="handleUserDeleted"
          @task-completed="updateTask">
          <!-- 使用具名插槽自定義用戶信息 -->
          <template #user-badge="{ user }">
            <span class="user-badge" :class="user.role">
              {{ user.role === 'admin' ? '👑' : '👤' }} {{ user.role }}
            </span>
          </template>
        </UserList>
      </div>
    </div>

    <!-- 組件通信演示 -->
    <div class="practice-section">
      <h2>📡 組件通信演示</h2>
      <div class="communication-demo">
        <ParentComponent @task-completed="updateTask" />
      </div>
    </div>

    <!-- 代碼展示 -->
    <div class="code-section">
      <h2>💻 關鍵代碼展示</h2>
      <div class="code-examples">
        <div class="code-example">
          <h4>Props 定義與使用</h4>
          <pre><code>// 子組件中定義 props
          const props = defineProps({
          article: {
          type: Object,
          required: true
          },
          showActions: {
          type: Boolean,
          default: true
          }
          })

          // 父組件中傳遞 props
          &lt;ArticleCard
          :article="articleData"
          :show-actions="true"
          /&gt;</code></pre>
        </div>

        <div class="code-example">
          <h4>事件發射與監聽</h4>
          <pre><code>// 子組件中發射事件
          const emit = defineEmits(['like', 'delete'])

          const handleLike = () => {
          emit('like', props.article.id)
          }

          // 父組件中監聽事件
          &lt;ArticleCard
          @like="handleLike"
          @delete="handleDelete"
          /&gt;</code></pre>
        </div>

        <div class="code-example">
          <h4>插槽使用</h4>
          <pre v-pre><code>// 子組件中定義插槽
          &lt;template&gt;
          &lt;div class="card"&gt;
          &lt;slot name="header"&gt;&lt;/slot&gt;
          &lt;slot&gt;&lt;/slot&gt;
          &lt;slot name="actions" :user="user"&gt;&lt;/slot&gt;
          &lt;/div&gt;
          &lt;/template&gt;

          // 父組件中使用插槽
          &lt;UserCard&gt;
          &lt;template #header&gt;用戶信息&lt;/template&gt;
          &lt;p&gt;用戶詳情&lt;/p&gt;
          &lt;template #actions="{ user }"&gt;
          &lt;button&gt;編輯 {{ user.name }}&lt;/button&gt;
          &lt;/template&gt;
          &lt;/UserCard&gt;</code></pre>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import ArticleEditor from './components/ArticleEditor.vue'
import ArticleCard from './components/ArticleCard.vue'
import StatsPanel from './components/StatsPanel.vue'
import UserForm from './components/UserForm.vue'
import UserList from './components/UserList.vue'
import ParentComponent from './components/ParentComponent.vue'

// 任務完成狀態
const tasks = ref({
  propsUsage: false,
  eventEmit: false,
  slotUsage: false,
  componentComposition: false
})

// 文章數據
const articles = ref([
  {
    id: 1,
    title: 'Vue 3 組件化開發指南',
    content: '學習如何使用Vue 3進行組件化開發，包括props、events、slots等核心概念。',
    author: '張小明',
    likes: 15,
    createdAt: new Date('2024-01-15')
  },
  {
    id: 2,
    title: 'Composition API 實戰',
    content: 'Composition API是Vue 3的新特性，讓我們的代碼更加靈活和可重用。',
    author: '李小華',
    likes: 23,
    createdAt: new Date('2024-01-20')
  }
])

// 用戶數據
const users = ref([
  {
    id: 1,
    name: '張小明',
    email: 'zhang@example.com',
    role: 'admin',
    avatar: '👨‍💼'
  },
  {
    id: 2,
    name: '李小華',
    email: 'li@example.com',
    role: 'user',
    avatar: '👩‍💻'
  }
])

// 計算屬性
const totalLikes = computed(() => {
  return articles.value.reduce((sum, article) => sum + article.likes, 0)
})

const mostLikedArticle = computed(() => {
  if (articles.value.length === 0) return null
  return articles.value.reduce((max, article) =>
    article.likes > max.likes ? article : max
  )
})

// 文章相關方法
const handleArticleCreated = (newArticle) => {
  articles.value.push({
    ...newArticle,
    id: Date.now(),
    likes: 0,
    createdAt: new Date()
  })
}

const handleLike = (articleId) => {
  const article = articles.value.find(a => a.id === articleId)
  if (article) {
    article.likes++
  }
}

const handleDelete = (articleId) => {
  const index = articles.value.findIndex(a => a.id === articleId)
  if (index > -1) {
    articles.value.splice(index, 1)
  }
}

const shareArticle = (article) => {
  alert(`分享文章: ${article.title}`)
}

// 用戶相關方法
const handleUserAdded = (newUser) => {
  users.value.push({
    ...newUser,
    id: Date.now()
  })
}

const handleUserUpdated = (updatedUser) => {
  const index = users.value.findIndex(u => u.id === updatedUser.id)
  if (index > -1) {
    users.value[index] = updatedUser
  }
}

const handleUserDeleted = (userId) => {
  const index = users.value.findIndex(u => u.id === userId)
  if (index > -1) {
    users.value.splice(index, 1)
  }
}

// 任務更新方法
const updateTask = (taskName) => {
  tasks.value[taskName] = true
}
</script>

<style scoped>
.component-practice {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.practice-header {
  text-align: center;
  margin-bottom: 30px;
  padding: 20px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border-radius: 15px;
}

.practice-header h1 {
  margin: 0 0 10px 0;
  font-size: 2.5em;
}

.task-section {
  background: #f8f9fa;
  padding: 20px;
  border-radius: 10px;
  margin-bottom: 30px;
}

.task-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 15px;
  margin-top: 15px;
}

.task-item {
  padding: 15px;
  background: white;
  border-radius: 8px;
  border-left: 4px solid #ddd;
  transition: all 0.3s ease;
}

.task-item.completed {
  border-left-color: #28a745;
  background: #f8fff9;
}

.practice-section {
  margin-bottom: 40px;
  padding: 25px;
  background: white;
  border-radius: 12px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}

.practice-section h2 {
  color: #333;
  margin-bottom: 20px;
  padding-bottom: 10px;
  border-bottom: 2px solid #eee;
}

.practice-section h3 {
  color: #555;
  margin-bottom: 15px;
}

.editor-section,
.articles-section,
.stats-section {
  margin-bottom: 30px;
}

.articles-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 20px;
  margin-top: 15px;
}

.action-btn {
  padding: 8px 16px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  font-size: 14px;
  transition: all 0.3s ease;
}

.share-btn {
  background: #17a2b8;
  color: white;
}

.share-btn:hover {
  background: #138496;
  transform: translateY(-2px);
}

.user-management {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 30px;
  align-items: start;
}

.user-badge {
  padding: 4px 8px;
  border-radius: 12px;
  font-size: 12px;
  font-weight: bold;
}

.user-badge.admin {
  background: #ffd700;
  color: #333;
}

.user-badge.user {
  background: #e3f2fd;
  color: #1976d2;
}

.communication-demo {
  padding: 20px;
  background: #f8f9fa;
  border-radius: 10px;
}

.code-section {
  background: #2d3748;
  color: white;
  padding: 25px;
  border-radius: 12px;
  margin-top: 30px;
}

.code-section h2 {
  color: #fff;
  margin-bottom: 20px;
}

.code-examples {
  display: grid;
  gap: 25px;
}

.code-example {
  background: #1a202c;
  padding: 20px;
  border-radius: 8px;
  border-left: 4px solid #4299e1;
}

.code-example h4 {
  color: #4299e1;
  margin-bottom: 15px;
  font-size: 1.1em;
}

.code-example pre {
  margin: 0;
  overflow-x: auto;
}

.code-example code {
  font-family: 'Fira Code', 'Consolas', monospace;
  font-size: 14px;
  line-height: 1.5;
  color: #e2e8f0;
}

@media (max-width: 768px) {
  .user-management {
    grid-template-columns: 1fr;
  }

  .articles-grid {
    grid-template-columns: 1fr;
  }

  .task-list {
    grid-template-columns: 1fr;
  }
}
</style>
