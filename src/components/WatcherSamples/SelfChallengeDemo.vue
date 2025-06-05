<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - Watcher 觀察者</h2>
    <p class="route-info">📍 路徑：/WatcherSamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>挑戰任務：</strong>建立一個數據監控系統，練習 watch 和 watchEffect 的使用
    </p>

    <div class="challenge-section">
      <h3>🎯 挑戰清單</h3>
      <div class="task-list">
        <div class="task-item">
          <input type="checkbox" id="task1">
          <label for="task1">1. 使用 watch 監控基本數據變化</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task2">
          <label for="task2">2. 實作深度監控（deep watch）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task3">
          <label for="task3">3. 使用 watchEffect 自動追蹤依賴</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task4">
          <label for="task4">4. 實作條件性監控和停止監控</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task5">
          <label for="task5">5. 監控多個數據源並做出響應</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task6">
          <label for="task6">6. 建立完整的數據監控日誌系統</label>
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
            <span class="function-name">userLevel (computed)</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            計算用戶等級邏輯（基於年齡和活躍度）
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>年齡分段：</strong>18歲以下(Youth)、18-30歲(Adult)、30-50歲(Senior)、50歲以上(Elder)</li>
                <li><strong>活躍度等級：</strong>0-25%(Low)、26-50%(Medium)、51-75%(High)、76-100%(VeryHigh)</li>
                <li><strong>等級計算：</strong>
                  <ul>
                    <li>Bronze: Youth + Low/Medium 或 Adult + Low</li>
                    <li>Silver: Adult + Medium/High 或 Senior + Low/Medium</li>
                    <li>Gold: Senior + High 或 Elder + Medium/High 或 Adult + VeryHigh</li>
                    <li>Platinum: Elder + VeryHigh 或 Senior + VeryHigh</li>
                  </ul>
                </li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作基本的 watch 監控用戶名變化</li>
                <li>學習 watch 的基本語法和用法</li>
                <li>處理新值和舊值的比較</li>
                <li>記錄監控日誌到系統中</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">2.</span>
            <span class="function-name">addLog(type, message)</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            實作添加日誌的輔助函數
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>參數：</strong>type (string): 日誌類型, message (string): 日誌訊息</li>
                <li><strong>日誌格式：</strong>{ time: string, type: string, message: string }</li>
                <li><strong>時間格式：</strong>使用 new Date().toLocaleTimeString() 產生 HH:MM:SS 格式</li>
                <li><strong>操作：</strong>將日誌物件推入 logs.value 陣列，並將 totalChanges.value += 1</li>
                <li><strong>日誌類型：</strong>'watch', 'watchEffect', 'deep', 'activity', 'multiple'</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作深度監控（deep watch）功能</li>
                <li>監控整個物件的變化</li>
                <li>使用 { deep: true } 選項</li>
                <li>處理物件屬性的深層變化</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">3.</span>
            <span class="function-name">watchUserName()</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            使用 watch 監控 user.name 的變化
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>監控對象：</strong>() => user.name (使用 getter 函數)</li>
                <li><strong>觸發條件：</strong>僅在 watchSettings.enableNameWatch 為 true 時啟用</li>
                <li><strong>日誌內容：</strong>`用戶名從 "${oldValue}" 變更為 "${newValue}"`</li>
                <li><strong>選項：</strong>{ immediate: false } (不立即執行)</li>
                <li><strong>返回值：</strong>將停止函數存入 watchers.value 陣列</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>使用 watchEffect 自動追蹤依賴</li>
                <li>理解自動依賴收集的概念</li>
                <li>處理多個數據源的自動追蹤</li>
                <li>學習 watchEffect 與 watch 的差異</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">4.</span>
            <span class="function-name">watchUserDeep()</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            使用 watch 深度監控整個 user 對象
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>監控對象：</strong>user (reactive 對象)</li>
                <li><strong>觸發條件：</strong>僅在 watchSettings.enableDeepWatch 為 true 時啟用</li>
                <li><strong>選項：</strong>{ deep: true, immediate: false }</li>
                <li><strong>日誌內容：</strong>`用戶資料發生深度變化 (等級: ${userLevel.value})`</li>
                <li><strong>日誌類型：</strong>'deep'</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作條件性監控功能</li>
                <li>根據設定動態啟用/停用監控器</li>
                <li>實作監控器的停止和重啟功能</li>
                <li>管理多個監控器的生命週期</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">5.</span>
            <span class="function-name">watchActivityLevel()</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            監控 user.activityLevel 的變化
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>監控對象：</strong>() => user.activityLevel</li>
                <li><strong>觸發條件：</strong>僅在 watchSettings.enableActivityWatch 為 true 時啟用</li>
                <li><strong>選項：</strong>{ immediate: true } (立即執行一次)</li>
                <li><strong>特殊邏輯：</strong>
                  <ul>
                    <li>活躍度 >= 80: `🔥 用戶活躍度極高！(${newValue}%)`</li>
                    <li>活躍度 >= 60: `⚡ 用戶活躍度良好 (${newValue}%)`</li>
                    <li>活躍度 < 30: `😴 用戶活躍度偏低 (${newValue}%)`</li>
                    <li>其他: `📊 活躍度變更為 ${newValue}%`</li>
                  </ul>
                </li>
                <li><strong>日誌類型：</strong>'activity'</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>監控多個數據源的變化</li>
                <li>使用陣列形式同時監控多個值</li>
                <li>處理多個新值和舊值</li>
                <li>根據變化情況提供不同回應</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">6.</span>
            <span class="function-name">setupWatchEffect()</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            使用 watchEffect 自動追蹤用戶數據變化
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>自動追蹤：</strong>user.name, user.age, user.activityLevel, user.hobbies.length</li>
                <li><strong>觸發時機：</strong>任何被追蹤的數據發生變化時</li>
                <li><strong>日誌內容：</strong>`🤖 watchEffect: ${user.name}(${user.age}歲) 活躍度${user.activityLevel}%
                  興趣${user.hobbies.length}項`</li>
                <li><strong>日誌類型：</strong>'watchEffect'</li>
                <li><strong>返回值：</strong>將停止函數存入 watchers.value 陣列</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>建立完整的數據監控日誌系統</li>
                <li>整合所有監控功能</li>
                <li>實作日誌的清理和統計功能</li>
                <li>提供監控狀態的可視化展示</li>
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
            <pre><code>// 基本 watch 用法
watch(source, (newValue, oldValue) => {
  console.log(`從 ${oldValue} 變為 ${newValue}`)
})

// 監控 ref
const count = ref(0)
watch(count, (newCount) => {
  console.log('計數變為:', newCount)
})

// 監控 reactive 物件的屬性
watch(() => user.name, (newName) => {
  console.log('用戶名變為:', newName)
})

// 深度監控
watch(user, (newUser) => {
  console.log('用戶資料變化:', newUser)
}, { deep: true })

// 監控多個來源
watch([() => user.name, () => user.age], ([newName, newAge]) => {
  console.log('姓名或年齡變化:', newName, newAge)
})

// watchEffect 自動追蹤依賴
watchEffect(() => {
  console.log(`用戶 ${user.name} 的年齡是 ${user.age}`)
})

// 停止監控
const stopWatcher = watch(source, callback)
stopWatcher() // 停止監控

// 立即執行
watch(source, callback, { immediate: true })</code></pre>

            <h5>重要概念：</h5>
            <ul>
              <li><strong>監控設定：</strong>注意檢查 watchSettings 的狀態來決定是否啟用特定的監控器</li>
              <li><strong>日誌格式：</strong>日誌對象應包含 { time, type, message } 三個屬性</li>
              <li><strong>時間格式：</strong>可以使用 new Date().toLocaleTimeString() 來格式化時間</li>
              <li><strong>監控器管理：</strong>將所有監控器的停止函數保存到 watchers.value 陣列中</li>
              <li><strong>條件監控：</strong>可以在監控函數內部檢查對應的設定狀態</li>
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
