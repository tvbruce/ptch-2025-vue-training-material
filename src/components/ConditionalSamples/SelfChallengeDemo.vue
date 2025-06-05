<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - v-if 條件渲染</h2>
    <p class="route-info">📍 路徑：/ConditionalSamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>挑戰任務：</strong>建立一個智能內容管理系統，練習各種條件渲染技巧
    </p>

    <div class="challenge-section">
      <h3>🎯 挑戰清單</h3>
      <div class="task-list">
        <div class="task-item">
          <input type="checkbox" id="task1">
          <label for="task1">1. 使用 v-if、v-else-if、v-else 實作多重條件</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task2">
          <label for="task2">2. 使用 v-show 實作頻繁切換的內容</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task3">
          <label for="task3">3. 使用 template 標籤包裝多個元素</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task4">
          <label for="task4">4. 實作複雜的條件邏輯組合</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task5">
          <label for="task5">5. 結合條件渲染與列表渲染</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task6">
          <label for="task6">6. 建立完整的用戶權限管理系統</label>
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
            <span class="function-name">shouldShowWelcome (computed)</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            根據用戶登入狀態決定是否顯示歡迎訊息
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>條件：</strong>isLoggedIn.value === true</li>
                <li><strong>返回值：</strong>boolean - 已登入返回 true</li>
                <li><strong>用途：</strong>控制歡迎區塊的 v-if 顯示</li>
                <li><strong>額外邏輯：</strong>可以加入時間判斷（如工作時間才顯示）</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>根據用戶登入狀態顯示不同內容</li>
                <li>實作多層條件判斷</li>
                <li>使用 template 標籤包裝多個元素</li>
                <li>處理複雜的條件邏輯</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">2.</span>
            <span class="function-name">getUserTypeMessage (computed)</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            根據用戶類型返回對應的歡迎訊息
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>guest：</strong>'歡迎訪客，請先登入以獲得完整體驗'</li>
                <li><strong>user：</strong>'歡迎回來！希望您今天過得愉快'</li>
                <li><strong>vip：</strong>'歡迎尊貴的VIP用戶，享受專屬服務'</li>
                <li><strong>admin：</strong>'歡迎管理員，您擁有完整的系統權限'</li>
                <li><strong>返回值：</strong>string - 對應的歡迎訊息</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作標籤頁切換功能</li>
                <li>控制模態框的顯示/隱藏</li>
                <li>理解 v-if 與 v-show 的性能差異</li>
                <li>實作動畫過渡效果</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">3.</span>
            <span class="function-name">getAvailableFeatures (computed)</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            根據用戶狀態和權限返回可用功能列表
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>guest：</strong>['瀏覽公開內容', '註冊帳號']</li>
                <li><strong>user：</strong>['個人資料', '發表評論', '收藏內容']</li>
                <li><strong>vip：</strong>user功能 + ['下載資源', '優先客服', 'VIP專區']</li>
                <li><strong>admin：</strong>所有功能 + ['用戶管理', '系統設定', '數據統計']</li>
                <li><strong>特殊權限：</strong>額外添加 ['測試功能', '開發工具']</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>根據條件篩選並顯示列表項目</li>
                <li>實作空狀態提示</li>
                <li>動態顯示載入狀態</li>
                <li>處理錯誤狀態顯示</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">4.</span>
            <span class="function-name">canAccessFeature(feature)</span>
            <span class="difficulty hard">困難</span>
          </div>
          <div class="function-description">
            檢查用戶是否有權限訪問特定功能
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>參數：</strong>feature (string) - 功能名稱</li>
                <li><strong>權限等級：</strong>
                  <ul>
                    <li>'public': 所有人可訪問</li>
                    <li>'user': 需要登入</li>
                    <li>'vip': 需要VIP身份</li>
                    <li>'admin': 僅管理員</li>
                  </ul>
                </li>
                <li><strong>返回值：</strong>boolean - 有權限返回 true</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
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

    <!-- 學員練習區塊 -->
    <div class="demo-section">
      <h3>🔧 學員練習區域</h3>
      <p class="hint">
        💡 <strong>提示：</strong>請根據上方的實作練習詳情完成以下功能實作
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
                <p>請使用 v-show 實作標籤頁切換效果</p>

                <!-- 提示：實作要求
                - 使用 v-show 控制標籤頁內容顯示
                - 每個標籤頁有不同的內容
                - 實作平滑的切換動畫
                - 保持未顯示標籤頁的狀態
                -->
              </div>
            </div>

            <!-- TODO: 實作模態框 -->
            <div v-show="showModal" class="modal-overlay">
              <div class="modal-content">
                <h4>模態框標題</h4>
                <p>這是一個使用 v-show 控制的模態框</p>
                <button @click="showModal = false" class="btn btn-secondary">關閉</button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, onMounted } from 'vue'

// TODO: 學員需要在這裡實作響應式變數和函數

// 用戶狀態
const userStatus = ref('guest')
const isLoggedIn = ref(false)
const hasPermission = ref(false)

// 標籤頁狀態
const activeTab = ref('tab1')
const showModal = ref(false)

// 標籤頁資料
const tabs = reactive([
  { id: 'tab1', title: '首頁', content: '這是首頁內容' },
  { id: 'tab2', title: '產品', content: '這是產品頁面內容' },
  { id: 'tab3', title: '關於', content: '這是關於我們的內容' }
])

// TODO: 實作計算屬性
// const shouldShowWelcome = computed(() => {
//   // 實作歡迎訊息顯示邏輯
// })

// const getUserTypeMessage = computed(() => {
//   // 實作用戶類型訊息
// })

// const getAvailableFeatures = computed(() => {
//   // 實作可用功能列表
// })

// TODO: 實作函數
// const canAccessFeature = (feature) => {
//   // 實作權限檢查邏輯
// }

onMounted(() => {
  console.log('條件渲染自我試煉載入完成')
})
</script>

<style scoped>
@import '@/assets/main.css';

/* 任務區塊樣式 */
.task-section {
  background: white;
  border-radius: 12px;
  padding: 1.5rem;
  margin: 1.5rem 0;
  border: 2px solid #e9ecef;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.practice-area {
  background: #f8f9fa;
  padding: 1.5rem;
  border-radius: 8px;
  margin-top: 1rem;
}

/* 控制項樣式 */
.controls {
  display: flex;
  gap: 1rem;
  align-items: center;
  margin-bottom: 1rem;
  flex-wrap: wrap;
}

.select-field {
  padding: 0.5rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  min-width: 120px;
}

.checkbox-label {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  cursor: pointer;
}

/* 用戶儀表板樣式 */
.user-dashboard {
  background: white;
  border-radius: 8px;
  padding: 1.5rem;
  border: 1px solid #e0e0e0;
}

.welcome-section,
.feature-section {
  margin-bottom: 1.5rem;
  padding: 1rem;
  background: #f8f9fa;
  border-radius: 8px;
}

.feature-list {
  margin-top: 1rem;
}

/* 標籤頁樣式 */
.tab-buttons {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.tab-btn {
  padding: 0.5rem 1rem;
  border: 1px solid #ddd;
  background: white;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.tab-btn.active {
  background: #007bff;
  color: white;
  border-color: #007bff;
}

.tab-container {
  position: relative;
}

.tab-content {
  background: white;
  border-radius: 8px;
  padding: 1.5rem;
  border: 1px solid #e0e0e0;
  min-height: 200px;
}

.tab-panel {
  transition: opacity 0.3s ease;
}

/* 模態框樣式 */
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
  border-radius: 8px;
  padding: 2rem;
  max-width: 400px;
  width: 90%;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
}

.btn {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.3s ease;
}

.btn-secondary {
  background: #6c757d;
  color: white;
}

.btn-secondary:hover {
  background: #5a6268;
}
</style>
