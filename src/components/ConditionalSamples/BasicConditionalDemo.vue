<template>
  <div class="basic-conditional-demo">
    <h2>基礎條件渲染</h2>
    <p class="route-info">📍 路徑：/ConditionalSamples/BasicConditionalDemo.vue</p>
    <p class="description">
      學習 Vue 的基本條件渲染指令及其使用方法
    </p>

    <!-- 1. 簡單的 v-if -->
    <div class="demo-section">
      <h3>1. 基本 v-if 用法</h3>
      <div class="controls">
        <label class="checkbox-label">
          <input type="checkbox" v-model="showMessage">
          顯示訊息
        </label>
      </div>
      <div class="result">
        <div v-if="showMessage" class="message success">
          ✅ 這是一個條件顯示的訊息！
        </div>
        <div v-else class="message info">
          ℹ️ 訊息已隱藏，勾選上方選項來顯示
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>&lt;div v-if="showMessage"&gt;顯示的內容&lt;/div&gt;
&lt;div v-else&gt;隱藏時的替代內容&lt;/div&gt;</code></pre>
      </div>
    </div>

    <!-- 2. v-if, v-else-if, v-else -->
    <div class="demo-section">
      <h3>2. 多條件判斷 (v-if / v-else-if / v-else)</h3>
      <div class="controls">
        <label>選擇分數範圍：</label>
        <select v-model="score" class="select-input">
          <option value="95">95 分</option>
          <option value="85">85 分</option>
          <option value="75">75 分</option>
          <option value="65">65 分</option>
          <option value="45">45 分</option>
        </select>
      </div>
      <div class="result">
        <div v-if="score >= 90" class="grade excellent">
          🏆 優秀！分數：{{ score }}
        </div>
        <div v-else-if="score >= 80" class="grade good">
          👍 良好！分數：{{ score }}
        </div>
        <div v-else-if="score >= 70" class="grade average">
          👌 普通，分數：{{ score }}
        </div>
        <div v-else-if="score >= 60" class="grade poor">
          😐 及格，分數：{{ score }}
        </div>
        <div v-else class="grade fail">
          😞 不及格，分數：{{ score }}
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>&lt;div v-if="score >= 90"&gt;優秀&lt;/div&gt;
&lt;div v-else-if="score >= 80"&gt;良好&lt;/div&gt;
&lt;div v-else-if="score >= 70"&gt;普通&lt;/div&gt;
&lt;div v-else-if="score >= 60"&gt;及格&lt;/div&gt;
&lt;div v-else&gt;不及格&lt;/div&gt;</code></pre>
      </div>
    </div>

    <!-- 3. 用戶狀態示例 -->
    <div class="demo-section">
      <h3>3. 用戶狀態管理</h3>
      <div class="controls">
        <label>用戶狀態：</label>
        <div class="radio-group">
          <label class="radio-label">
            <input type="radio" v-model="userStatus" value="guest">
            訪客
          </label>
          <label class="radio-label">
            <input type="radio" v-model="userStatus" value="user">
            普通用戶
          </label>
          <label class="radio-label">
            <input type="radio" v-model="userStatus" value="vip">
            VIP 用戶
          </label>
          <label class="radio-label">
            <input type="radio" v-model="userStatus" value="admin">
            管理員
          </label>
        </div>
      </div>
      <div class="result">
        <div class="user-panel">
          <div v-if="userStatus === 'guest'" class="user-info guest">
            <h4>👋 歡迎訪客</h4>
            <p>請登入以獲得更多功能</p>
            <button class="btn btn-primary">立即登入</button>
          </div>

          <div v-else-if="userStatus === 'user'" class="user-info user">
            <h4>😊 歡迎用戶</h4>
            <p>您可以瀏覽基本內容</p>
            <div class="features">
              <span class="feature">✅ 基本瀏覽</span>
              <span class="feature">✅ 個人資料</span>
            </div>
          </div>

          <div v-else-if="userStatus === 'vip'" class="user-info vip">
            <h4>⭐ 歡迎 VIP</h4>
            <p>享受專屬 VIP 服務</p>
            <div class="features">
              <span class="feature">✅ 所有基本功能</span>
              <span class="feature">✅ 專屬內容</span>
              <span class="feature">✅ 優先客服</span>
            </div>
          </div>

          <div v-else-if="userStatus === 'admin'" class="user-info admin">
            <h4>🔧 管理員面板</h4>
            <p>系統管理權限</p>
            <div class="features">
              <span class="feature">✅ 用戶管理</span>
              <span class="feature">✅ 系統設定</span>
              <span class="feature">✅ 數據分析</span>
            </div>
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>&lt;div v-if="userStatus === 'guest'"&gt;訪客內容&lt;/div&gt;
&lt;div v-else-if="userStatus === 'user'"&gt;用戶內容&lt;/div&gt;
&lt;div v-else-if="userStatus === 'vip'"&gt;VIP 內容&lt;/div&gt;
&lt;div v-else-if="userStatus === 'admin'"&gt;管理員內容&lt;/div&gt;</code></pre>
      </div>
    </div>

    <!-- 4. 複雜條件 -->
    <div class="demo-section">
      <h3>4. 複雜條件組合</h3>
      <div class="controls">
        <div class="control-group">
          <label class="checkbox-label">
            <input type="checkbox" v-model="isLoggedIn">
            已登入
          </label>
          <label class="checkbox-label">
            <input type="checkbox" v-model="hasPermission">
            有權限
          </label>
          <label class="checkbox-label">
            <input type="checkbox" v-model="isActive">
            帳號啟用
          </label>
        </div>
      </div>
      <div class="result">
        <div v-if="isLoggedIn && hasPermission && isActive" class="status success">
          🎉 歡迎！您可以訪問所有功能
        </div>
        <div v-else-if="isLoggedIn && !isActive" class="status warning">
          ⚠️ 請先啟用您的帳號
        </div>
        <div v-else-if="isLoggedIn && !hasPermission" class="status error">
          🚫 您沒有訪問權限
        </div>
        <div v-else class="status info">
          🔐 請先登入系統
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>&lt;div v-if="isLoggedIn && hasPermission && isActive"&gt;
  全部條件滿足
&lt;/div&gt;
&lt;div v-else-if="isLoggedIn && !isActive"&gt;
  已登入但未啟用
&lt;/div&gt;
&lt;div v-else-if="isLoggedIn && !hasPermission"&gt;
  已登入但無權限
&lt;/div&gt;
&lt;div v-else&gt;
  未登入
&lt;/div&gt;</code></pre>
      </div>
    </div>

    <!-- 重點提醒 -->
    <div class="tips-section">
      <h3>💡 重點提醒</h3>
      <div class="tips-grid">
        <div class="tip-item">
          <h4>條件渲染的特性</h4>
          <ul>
            <li>v-if 是真正的條件渲染，會創建/銷毀元素</li>
            <li>v-else-if 和 v-else 必須緊跟在 v-if 後面</li>
            <li>可以在 &lt;template&gt; 上使用，不會渲染額外元素</li>
          </ul>
        </div>
        <div class="tip-item">
          <h4>性能考量</h4>
          <ul>
            <li>v-if 有更高的切換開銷</li>
            <li>如果條件很少改變，使用 v-if</li>
            <li>如果需要頻繁切換，考慮使用 v-show</li>
          </ul>
        </div>
        <div class="tip-item">
          <h4>最佳實踐</h4>
          <ul>
            <li>避免 v-if 和 v-for 同時使用</li>
            <li>複雜條件可以提取為計算屬性</li>
            <li>使用 key 屬性強制重新渲染</li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// 基本顯示控制
const showMessage = ref(true)

// 分數等級
const score = ref(85)

// 用戶狀態
const userStatus = ref('guest')

// 複雜條件
const isLoggedIn = ref(false)
const hasPermission = ref(false)
const isActive = ref(false)
</script>

<style scoped>
/* 組件樣式已在全域 main.css 中定義 */
</style>
