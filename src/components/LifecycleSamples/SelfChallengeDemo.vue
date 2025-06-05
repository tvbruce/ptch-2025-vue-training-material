<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - Lifecycle 生命週期</h2>
    <p class="route-info">📍 路徑：/LifecycleSamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>挑戰任務：</strong>練習 Vue3 生命週期鉤子的基本用法
    </p>

    <div class="challenge-section">
      <h3>🎯 挑戰清單</h3>
      <div class="task-list">
        <div class="task-item">
          <input type="checkbox" id="task1">
          <label for="task1">1. 實作基本計時器（onMounted & onUnmounted）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task2">
          <label for="task2">2. 實作數據載入功能（onMounted）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task3">
          <label for="task3">3. 實作更新計數器（onUpdated）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task4">
          <label for="task4">4. 實作計時器控制功能</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task5">
          <label for="task5">5. 實作資源清理邏輯</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task6">
          <label for="task6">6. 建立完整的生命週期管理系統</label>
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
            <span class="function-name">formatTime(seconds)</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            將秒數轉換為 "mm:ss" 格式
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>參數：</strong>seconds (number) - 總秒數</li>
                <li><strong>計算：</strong>分鐘 = Math.floor(seconds / 60)</li>
                <li><strong>計算：</strong>秒數 = seconds % 60</li>
                <li><strong>格式：</strong>使用 padStart(2, '0') 補零</li>
                <li><strong>返回：</strong>格式化字串，例如 "01:30"</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作時間格式化函數</li>
                <li>處理分鐘和秒數的計算</li>
                <li>確保時間顯示格式正確</li>
                <li>使用 padStart 方法補零</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">2.</span>
            <span class="function-name">toggleTimer()</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            控制計時器的開始和暫停
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>狀態檢查：</strong>根據 isTimerRunning.value 決定操作</li>
                <li><strong>開始計時：</strong>設定 setInterval，每秒增加 timerSeconds.value</li>
                <li><strong>暫停計時：</strong>清除 interval，保存 intervalId</li>
                <li><strong>狀態更新：</strong>切換 isTimerRunning.value</li>
                <li><strong>清理：</strong>確保舊的 interval 被正確清除</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作計時器的開始和暫停功能</li>
                <li>管理 setInterval 和 clearInterval</li>
                <li>正確更新計時器狀態</li>
                <li>防止記憶體洩漏</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">3.</span>
            <span class="function-name">resetTimer()</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            重置計時器為初始狀態
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>停止計時：</strong>清除 intervalId</li>
                <li><strong>重置時間：</strong>timerSeconds.value = 0</li>
                <li><strong>重置狀態：</strong>isTimerRunning.value = false</li>
                <li><strong>清理資源：</strong>確保沒有殘留的 interval</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>重置計時器到初始狀態</li>
                <li>清理所有計時器資源</li>
                <li>重置相關狀態變數</li>
                <li>確保功能的完整性</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">4.</span>
            <span class="function-name">loadUserData()</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            模擬載入用戶資料
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>載入狀態：</strong>設定 isLoading.value = true</li>
                <li><strong>模擬延遲：</strong>使用 setTimeout 模擬 2 秒載入時間</li>
                <li><strong>模擬資料：</strong>建立包含 id, name, email 的用戶陣列</li>
                <li><strong>完成載入：</strong>設定 userData.value 和 isLoading.value = false</li>
                <li><strong>錯誤處理：</strong>可選擇性加入錯誤處理邏輯</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>模擬異步數據載入過程</li>
                <li>管理載入狀態的顯示</li>
                <li>處理載入成功和失敗情況</li>
                <li>提供良好的用戶體驗</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">5.</span>
            <span class="function-name">onMounted 生命週期</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            組件掛載後的初始化邏輯
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>自動載入：</strong>調用 loadUserData() 載入初始資料</li>
                <li><strong>可選啟動：</strong>可以選擇自動啟動計時器</li>
                <li><strong>日誌記錄：</strong>console.log 記錄組件掛載</li>
                <li><strong>初始化：</strong>設定任何需要的初始狀態</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作組件掛載後的初始化邏輯</li>
                <li>自動載入必要的初始數據</li>
                <li>設定組件的初始狀態</li>
                <li>記錄組件生命週期事件</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">6.</span>
            <span class="function-name">onUnmounted 生命週期</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            組件卸載前的清理邏輯
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>清理計時器：</strong>清除所有 setInterval</li>
                <li><strong>重置狀態：</strong>重置所有相關狀態</li>
                <li><strong>日誌記錄：</strong>console.log 記錄組件卸載</li>
                <li><strong>防止洩漏：</strong>確保沒有記憶體洩漏</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作組件卸載前的清理邏輯</li>
                <li>清理所有計時器和訂閱</li>
                <li>防止記憶體洩漏問題</li>
                <li>確保資源正確釋放</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">7.</span>
            <span class="function-name">onUpdated 生命週期</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            組件更新後的邏輯
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>更新計數：</strong>增加 updateCount.value</li>
                <li><strong>日誌記錄：</strong>記錄更新次數</li>
                <li><strong>可選邏輯：</strong>可以加入其他更新後的處理</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>監控組件的更新行為</li>
                <li>記錄組件更新次數</li>
                <li>理解什麼操作會觸發更新</li>
                <li>實作更新後的處理邏輯</li>
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
            <pre><code>// 組件生命週期
import { onMounted, onUnmounted, onUpdated } from 'vue'

// onMounted: 組件掛載完成後執行
onMounted(() => {
  console.log('組件已掛載')
  // 啟動計時器、載入數據等
})

// onUnmounted: 組件卸載前執行
onUnmounted(() => {
  console.log('組件即將卸載')
  // 清理計時器、取消訂閱等
})

// onUpdated: 組件更新後執行
onUpdated(() => {
  console.log('組件已更新')
})

// 計時器管理
const timer = setInterval(() => {
  // 每秒執行
}, 1000)
clearInterval(timer) // 清理計時器

// 時間格式化
const minutes = Math.floor(seconds / 60)
const remainingSeconds = seconds % 60</code></pre>

            <h5>重要概念：</h5>
            <ul>
              <li><strong>計時器管理：</strong>使用 setInterval 和 clearInterval 管理計時器</li>
              <li><strong>生命週期：</strong>onMounted 用於初始化，onUnmounted 用於清理</li>
              <li><strong>狀態管理：</strong>合理使用 ref 管理組件狀態</li>
              <li><strong>記憶體管理：</strong>確保在組件卸載時清理所有資源</li>
              <li><strong>非同步處理：</strong>使用 setTimeout 模擬 API 呼叫</li>
            </ul>
          </div>
        </details>
      </div>
    </div>


  </div>
</template>

<script setup>
// 此文件僅包含自我試煉的題目說明和實作指引
// 實際的程式碼實作請在 SelfChallengeAnsweringArea.vue 中完成
</script>

<style scoped>
/* 使用統一的自我試煉樣式 */
@import '@/assets/main.css';
</style>
