<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - 條件渲染</h2>
    <p class="route-info">📍 路徑：/ConditionalSamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>挑戰任務：</strong>建立一個動態內容管理系統，練習各種條件渲染技巧
    </p>

    <div class="challenge-section">
      <h3>🎯 挑戰清單</h3>
      <div class="task-list">
        <div class="task-item">
          <input type="checkbox" id="task1">
          <label for="task1">1. 使用 v-if、v-else-if、v-else 控制內容顯示</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task2">
          <label for="task2">2. 使用 v-show 實作頻繁切換的內容</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task3">
          <label for="task3">3. 實作標籤頁切換功能</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task4">
          <label for="task4">4. 實作模態框顯示/隱藏</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task5">
          <label for="task5">5. 實作複雜的條件邏輯</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task6">
          <label for="task6">6. 建立完整的動態內容管理系統</label>
        </div>
      </div>
    </div>

    <div class="implementation-section">
      <h3>👨‍💻 實作練習詳情</h3>
      <p class="implementation-intro">
        📋 <strong>請在 &lt;script setup&gt; 區域完成以下函數的實作：</strong>
      </p>

      <div class="implementation-list">
        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">1.</span>
            <span class="function-name">userStatus (computed)</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            根據用戶資料計算狀態
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>未登入：</strong>user.isLoggedIn === false</li>
                <li><strong>一般用戶：</strong>已登入但 user.role === 'user'</li>
                <li><strong>管理員：</strong>已登入且 user.role === 'admin'</li>
                <li><strong>VIP 用戶：</strong>已登入且 user.role === 'vip'</li>
                <li><strong>返回值：</strong>字串 - 'guest', 'user', 'admin', 'vip'</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">2.</span>
            <span class="function-name">toggleLogin()</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            切換用戶登入狀態
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>切換狀態：</strong>反轉 user.isLoggedIn 的值</li>
                <li><strong>登出處理：</strong>如果變為未登入，重置 user.role 為 'user'</li>
                <li><strong>重置資料：</strong>登出時清空 user.name</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">3.</span>
            <span class="function-name">switchTab(tabName)</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            切換活躍的標籤頁
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>參數：</strong>tabName (string) - 要切換到的標籤名稱</li>
                <li><strong>更新狀態：</strong>設定 activeTab.value = tabName</li>
                <li><strong>有效標籤：</strong>'home', 'about', 'contact', 'settings'</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">4.</span>
            <span class="function-name">toggleModal()</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            切換模態框的顯示狀態
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>切換狀態：</strong>反轉 showModal.value 的值</li>
                <li><strong>動畫效果：</strong>可以加入淡入淡出效果</li>
                <li><strong>背景鎖定：</strong>模態框開啟時可以鎖定背景滾動</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">5.</span>
            <span class="function-name">updateUserRole(role)</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            更新用戶角色
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>參數：</strong>role (string) - 新的用戶角色</li>
                <li><strong>更新角色：</strong>設定 user.role = role</li>
                <li><strong>有效角色：</strong>'user', 'admin', 'vip'</li>
                <li><strong>權限檢查：</strong>只有已登入用戶才能更改角色</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">6.</span>
            <span class="function-name">canAccess(feature)</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            檢查用戶是否有權限存取特定功能
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>參數：</strong>feature (string) - 功能名稱</li>
                <li><strong>權限規則：</strong>
                  <ul>
                    <li>'basic': 所有已登入用戶</li>
                    <li>'premium': VIP 和管理員</li>
                    <li>'admin': 僅管理員</li>
                  </ul>
                </li>
                <li><strong>返回值：</strong>boolean - 有權限返回 true</li>
              </ul>
            </div>
          </div>
        </div>
      </div>

      <div class="hint-section">
        <h4>💡 開發提示</h4>
        <details>
          <summary>點擊查看開發提示</summary>
          <div class="hints">
            <h5>常用語法參考：</h5>
            <pre><code>// 基本條件渲染
&lt;div v-if="isLoggedIn"&gt;歡迎回來&lt;/div&gt;
&lt;div v-else&gt;請先登入&lt;/div&gt;

// 多重條件
&lt;div v-if="userType === 'admin'"&gt;管理員面板&lt;/div&gt;
&lt;div v-else-if="userType === 'vip'"&gt;VIP 專區&lt;/div&gt;
&lt;div v-else&gt;一般用戶&lt;/div&gt;

// template 包裝
&lt;template v-if="showDetails"&gt;
  &lt;h3&gt;詳細資訊&lt;/h3&gt;
  &lt;p&gt;內容描述&lt;/p&gt;
&lt;/template&gt;

// v-show 用於頻繁切換
&lt;div v-show="isVisible"&gt;切換顯示&lt;/div&gt;

// 條件組合
&lt;div v-if="user.isActive && user.hasPermission"&gt;
  有權限的活躍用戶
&lt;/div&gt;</code></pre>

            <h5>重要概念：</h5>
            <ul>
              <li><strong>v-if vs v-show：</strong>v-if 適合條件很少改變的情況，v-show 適合頻繁切換</li>
              <li><strong>template 標籤：</strong>可以用來包裝多個元素而不產生額外的 DOM 節點</li>
              <li><strong>複雜條件：</strong>可以使用計算屬性來簡化模板中的條件邏輯</li>
              <li><strong>性能考量：</strong>v-if 有更高的切換開銷，v-show 有更高的初始渲染開銷</li>
              <li><strong>條件組合：</strong>可以使用 && 和 || 運算子組合多個條件</li>
            </ul>
          </div>
        </details>
      </div>
    </div>

    <!-- 練習任務區塊 -->
    <div class="practice-requirements">
      <h3>📋 練習任務說明</h3>
      <div class="requirement-grid">
        <div class="requirement-card">
          <h4>🎯 任務一：基礎條件渲染</h4>
          <p><strong>目標：</strong>使用 v-if、v-else-if、v-else 控制內容顯示</p>
          <div class="specs">
            <h5>規格說明：</h5>
            <ul>
              <li>根據用戶登入狀態顯示不同內容</li>
              <li>實作多層條件判斷</li>
              <li>使用 template 標籤包裝多個元素</li>
              <li>處理複雜的條件邏輯</li>
            </ul>
          </div>
        </div>

        <div class="requirement-card">
          <h4>🎯 任務二：v-show 切換效果</h4>
          <p><strong>目標：</strong>使用 v-show 實作頻繁切換的內容</p>
          <div class="specs">
            <h5>規格說明：</h5>
            <ul>
              <li>實作標籤頁切換功能</li>
              <li>控制模態框的顯示/隱藏</li>
              <li>理解 v-if 與 v-show 的性能差異</li>
              <li>實作動畫過渡效果</li>
            </ul>
          </div>
        </div>

        <div class="requirement-card">
          <h4>🎯 任務三：條件列表渲染</h4>
          <p><strong>目標：</strong>結合條件渲染與列表渲染</p>
          <div class="specs">
            <h5>規格說明：</h5>
            <ul>
              <li>根據條件篩選並顯示列表項目</li>
              <li>實作空狀態提示</li>
              <li>動態顯示載入狀態</li>
              <li>處理錯誤狀態顯示</li>
            </ul>
          </div>
        </div>

        <div class="requirement-card">
          <h4>🎯 任務四：動態組件切換</h4>
          <p><strong>目標：</strong>使用條件渲染實作組件切換</p>
          <div class="specs">
            <h5>規格說明：</h5>
            <ul>
              <li>根據狀態動態載入不同組件</li>
              <li>實作權限控制顯示</li>
              <li>處理組件載入失敗情況</li>
              <li>優化組件切換性能</li>
            </ul>
          </div>
        </div>
      </div>
    </div>

    <!-- 學員練習區塊 -->
    <div class="demo-section">
      <h3>🔧 學員練習區域</h3>
      <p class="hint">
        💡 <strong>提示：</strong>請根據上方的任務說明完成以下功能實作
      </p>

      <!-- 任務一：基礎條件渲染 -->
      <div class="task-section">
        <h4>任務一：用戶狀態管理系統</h4>
        <div class="controls">
          <select v-model="userStatus" class="select-field">
            <option value="guest">訪客</option>
            <option value="user">一般用戶</option>
            <option value="vip">VIP用戶</option>
            <option value="admin">管理員</option>
          </select>

          <label class="checkbox-label">
            <input type="checkbox" v-model="isLoggedIn">
            已登入
          </label>

          <label class="checkbox-label">
            <input type="checkbox" v-model="hasPermission">
            有特殊權限
          </label>
        </div>

        <div class="practice-area">
          <div class="user-dashboard">
            <!-- TODO: 學員需要在這裡實作條件渲染 -->
            <div class="welcome-section">
              <h4>歡迎訊息區域</h4>
              <p>請根據用戶狀態顯示不同的歡迎訊息</p>

              <!-- 提示：實作邏輯
              - 未登入：顯示 "歡迎訪客，請先登入"
              - 一般用戶：顯示 "歡迎回來，[用戶名]"
              - VIP用戶：顯示 "歡迎尊貴的VIP用戶"
              - 管理員：顯示 "歡迎管理員，您有完整權限"
              -->
            </div>

            <div class="feature-section">
              <h4>功能區域</h4>
              <!-- TODO: 根據用戶狀態和權限顯示不同功能 -->
              <div class="feature-list">
                <p>請根據用戶狀態顯示可用功能</p>

                <!-- 提示：功能顯示邏輯
                - 訪客：只能瀏覽公開內容
                - 一般用戶：可以查看個人資料、發表評論
                - VIP用戶：額外可以下載資源、優先客服
                - 管理員：可以管理用戶、查看統計
                - 有特殊權限：可以訪問測試功能
                -->
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- 任務二：標籤頁切換系統 -->
      <div class="task-section">
        <h4>任務二：標籤頁切換系統</h4>
        <div class="controls">
          <div class="tab-buttons">
            <button v-for="tab in tabs" :key="tab.id" @click="activeTab = tab.id"
              :class="['tab-btn', { active: activeTab === tab.id }]">
              {{ tab.title }}
            </button>
          </div>

          <label class="checkbox-label">
            <input type="checkbox" v-model="showModal">
            顯示模態框
          </label>
        </div>

        <div class="practice-area">
          <div class="tab-container">
            <!-- TODO: 學員需要在這裡實作 v-show 標籤頁切換 -->
            <div class="tab-content">
              <div class="tab-panel">
                <h4>標籤頁內容</h4>
                <p>請使用 v-show 實作標籤頁切換</p>

                <!-- 提示：
                - 使用 v-show 控制每個標籤頁的顯示
                - 確保只有當前活躍的標籤頁可見
                - 添加 CSS 過渡效果
                -->
              </div>
            </div>

            <!-- TODO: 實作模態框 -->
            <div v-show="showModal" class="modal-overlay">
              <div class="modal-content">
                <h4>模態框標題</h4>
                <p>這是一個使用 v-show 控制的模態框</p>
                <button @click="showModal = false" class="close-btn">關閉</button>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- 任務三：動態列表管理 -->
      <div class="task-section">
        <h4>任務三：動態列表管理</h4>
        <div class="controls">
          <select v-model="listFilter" class="select-field">
            <option value="all">全部項目</option>
            <option value="active">活躍項目</option>
            <option value="completed">已完成項目</option>
            <option value="pending">待處理項目</option>
          </select>

          <button @click="toggleLoading" class="btn btn-primary">
            {{ isLoading ? '停止載入' : '模擬載入' }}
          </button>

          <button @click="toggleError" class="btn btn-warning">
            {{ hasError ? '清除錯誤' : '模擬錯誤' }}
          </button>
        </div>

        <div class="practice-area">
          <div class="list-container">
            <!-- TODO: 學員需要在這裡實作條件列表渲染 -->
            <div class="list-header">
              <h4>項目列表</h4>
              <p>總共 {{ items.length }} 個項目</p>
            </div>

            <div class="list-content">
              <!-- TODO: 實作以下條件渲染邏輯
              1. 載入狀態：顯示載入動畫
              2. 錯誤狀態：顯示錯誤訊息
              3. 空狀態：沒有符合條件的項目時顯示提示
              4. 正常狀態：顯示篩選後的項目列表
              -->

              <div class="placeholder">
                <p>請實作條件渲染邏輯</p>
                <ul>
                  <li>載入中：顯示 "載入中..." 訊息</li>
                  <li>發生錯誤：顯示 "載入失敗，請重試" 訊息</li>
                  <li>無資料：顯示 "沒有符合條件的項目" 訊息</li>
                  <li>有資料：顯示篩選後的項目列表</li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- 學習目標 -->
    <div class="learning-goals">
      <h4>🎯 學習目標</h4>
      <div class="goals-grid">
        <div class="goal-item">
          <span class="goal-icon">🔀</span>
          <span class="goal-text">掌握 v-if、v-else-if、v-else 的使用</span>
        </div>
        <div class="goal-item">
          <span class="goal-icon">👁️</span>
          <span class="goal-text">理解 v-show 與 v-if 的差異和適用場景</span>
        </div>
        <div class="goal-item">
          <span class="goal-icon">🎛️</span>
          <span class="goal-text">學會處理複雜的條件邏輯</span>
        </div>
        <div class="goal-item">
          <span class="goal-icon">📋</span>
          <span class="goal-text">掌握條件渲染與列表渲染的結合</span>
        </div>
        <div class="goal-item">
          <span class="goal-icon">⚡</span>
          <span class="goal-text">優化條件渲染的性能表現</span>
        </div>
        <div class="goal-item">
          <span class="goal-icon">🎨</span>
          <span class="goal-text">實作流暢的用戶界面切換效果</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 任務一：用戶狀態管理
const userStatus = ref('guest')
const isLoggedIn = ref(false)
const hasPermission = ref(false)

// 任務二：標籤頁切換
const activeTab = ref('home')
const showModal = ref(false)

const tabs = [
  { id: 'home', title: '首頁' },
  { id: 'profile', title: '個人資料' },
  { id: 'settings', title: '設定' },
  { id: 'help', title: '幫助' }
]

// 任務三：動態列表
const listFilter = ref('all')
const isLoading = ref(false)
const hasError = ref(false)

const items = ref([
  { id: 1, name: '項目 1', status: 'active' },
  { id: 2, name: '項目 2', status: 'completed' },
  { id: 3, name: '項目 3', status: 'pending' },
  { id: 4, name: '項目 4', status: 'active' },
  { id: 5, name: '項目 5', status: 'completed' }
])

// 計算屬性
const filteredItems = computed(() => {
  if (listFilter.value === 'all') return items.value
  return items.value.filter(item => item.status === listFilter.value)
})

// 供學員參考的計算屬性
console.log('filteredItems available for student use:', filteredItems)

// 方法
const toggleLoading = () => {
  isLoading.value = !isLoading.value
  if (isLoading.value) {
    hasError.value = false
  }
}

const toggleError = () => {
  hasError.value = !hasError.value
  if (hasError.value) {
    isLoading.value = false
  }
}
</script>

<style scoped>
/* 使用統一的自我試煉樣式 */
@import '@/assets/self-challenge.css';

/* 任務特定樣式 */
.task-section {
  margin: 2rem 0;
  padding: 1.5rem;
  background: white;
  border-radius: 10px;
  border: 1px solid #e0e0e0;
}

.task-section h4 {
  color: #2c3e50;
  margin-bottom: 1rem;
  padding-bottom: 0.5rem;
  border-bottom: 2px solid #3498db;
}

.practice-area {
  margin-top: 1rem;
  padding: 1rem;
  background: #f8f9fa;
  border-radius: 8px;
  border: 2px dashed #dee2e6;
}

.user-dashboard {
  background: white;
  border-radius: 8px;
  padding: 1.5rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.welcome-section,
.feature-section {
  margin-bottom: 1.5rem;
  padding: 1rem;
  border: 1px solid #e0e0e0;
  border-radius: 6px;
}

.feature-list {
  margin-top: 1rem;
}

.tab-buttons {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.tab-btn {
  padding: 0.5rem 1rem;
  border: 1px solid #ddd;
  background: white;
  border-radius: 4px 4px 0 0;
  cursor: pointer;
  transition: all 0.3s ease;
}

.tab-btn.active {
  background: #3498db;
  color: white;
  border-color: #3498db;
}

.tab-container {
  position: relative;
}

.tab-content {
  border: 1px solid #ddd;
  border-radius: 0 4px 4px 4px;
  background: white;
  min-height: 200px;
}

.tab-panel {
  padding: 1.5rem;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal-content {
  background: white;
  padding: 2rem;
  border-radius: 8px;
  max-width: 400px;
  width: 90%;
}

.close-btn {
  margin-top: 1rem;
  padding: 0.5rem 1rem;
  background: #e74c3c;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.list-container {
  background: white;
  border-radius: 8px;
  padding: 1.5rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.list-header {
  margin-bottom: 1rem;
  padding-bottom: 1rem;
  border-bottom: 1px solid #e0e0e0;
}

.list-content {
  min-height: 200px;
}

.placeholder {
  padding: 2rem;
  text-align: center;
  color: #666;
  background: #f8f9fa;
  border-radius: 6px;
  border: 2px dashed #ddd;
}

.placeholder ul {
  text-align: left;
  max-width: 400px;
  margin: 1rem auto;
}

.placeholder li {
  margin: 0.5rem 0;
  color: #555;
}
</style>
