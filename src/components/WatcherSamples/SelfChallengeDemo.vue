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
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">7.</span>
            <span class="function-name">watchMultipleSources()</span>
            <span class="difficulty hard">困難</span>
          </div>
          <div class="function-description">
            同時監控用戶名和年齡的變化
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>監控對象：</strong>[() => user.name, () => user.age] (數組形式)</li>
                <li><strong>回調參數：</strong>([newName, newAge], [oldName, oldAge])</li>
                <li><strong>日誌內容：</strong>
                  <ul>
                    <li>名字變化: `👤 用戶名: ${oldName} → ${newName}`</li>
                    <li>年齡變化: `🎂 年齡: ${oldAge} → ${newAge}`</li>
                    <li>同時變化: `📝 用戶資料更新: ${newName}(${newAge}歲)`</li>
                  </ul>
                </li>
                <li><strong>日誌類型：</strong>'multiple'</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">8.</span>
            <span class="function-name">clearLogs()</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            清除所有日誌記錄
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>操作 1：</strong>將 logs.value 設為空陣列 []</li>
                <li><strong>操作 2：</strong>將 totalChanges.value 重置為 0</li>
                <li><strong>提示：</strong>執行後應該會看到 "暫無監控日誌" 的訊息</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">9.</span>
            <span class="function-name">stopAllWatchers()</span>
            <span class="difficulty hard">困難</span>
          </div>
          <div class="function-description">
            停止所有活躍的監控器
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>操作：</strong>遍歷 watchers.value 陣列，調用每個停止函數</li>
                <li><strong>清理：</strong>執行完畢後將 watchers.value 設為空陣列</li>
                <li><strong>日誌：</strong>使用 addLog 記錄 `⏹️ 已停止所有監控器 (共${count}個)`</li>
                <li><strong>日誌類型：</strong>'watch'</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">10.</span>
            <span class="function-name">startAllWatchers()</span>
            <span class="difficulty hard">困難</span>
          </div>
          <div class="function-description">
            重新啟動所有監控器
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>前置作業：</strong>先調用 stopAllWatchers() 清除現有監控</li>
                <li><strong>條件啟動：</strong>根據 watchSettings 的狀態決定啟動哪些監控器：
                  <ul>
                    <li>enableNameWatch → 調用 watchUserName()</li>
                    <li>enableDeepWatch → 調用 watchUserDeep()</li>
                    <li>enableActivityWatch → 調用 watchActivityLevel()</li>
                  </ul>
                </li>
                <li><strong>固定啟動：</strong>總是調用 setupWatchEffect() 和 watchMultipleSources()</li>
                <li><strong>日誌：</strong>`🚀 已重新啟動監控系統`</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">11.</span>
            <span class="function-name">onUnmounted 清理</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            在組件卸載時清理所有監控器
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>清理時機：</strong>組件從 DOM 中移除之前</li>
                <li><strong>清理內容：</strong>調用 stopAllWatchers() 停止所有監控</li>
                <li><strong>防止記憶體洩漏：</strong>確保所有 watcher 都被正確清理</li>
                <li><strong>實作位置：</strong>在 onUnmounted(() => { ... }) 回調函數中</li>
              </ul>
            </div>
          </div>
        </div>
      </div>

      <div class="implementation-tips">
        <h4>🔧 實作提示</h4>
        <ul>
          <li><strong>監控設定：</strong>注意檢查 watchSettings 的狀態來決定是否啟用特定的監控器</li>
          <li><strong>日誌格式：</strong>日誌對象應包含 { time, type, message } 三個屬性</li>
          <li><strong>時間格式：</strong>可以使用 new Date().toLocaleTimeString() 來格式化時間</li>
          <li><strong>監控器管理：</strong>將所有監控器的停止函數保存到 watchers.value 陣列中</li>
          <li><strong>條件監控：</strong>可以在監控函數內部檢查對應的設定狀態</li>
        </ul>
      </div>
    </div>

    <div class="demo-section">
      <h3>📊 用戶行為監控</h3>
      <div class="user-controls">
        <div class="control-group">
          <label>用戶名：</label>
          <input v-model="user.name" placeholder="輸入用戶名" class="form-input">
        </div>

        <div class="control-group">
          <label>年齡：</label>
          <input v-model.number="user.age" type="number" placeholder="輸入年齡" class="form-input">
        </div>

        <div class="control-group">
          <label>興趣愛好：</label>
          <div class="hobby-list">
            <label v-for="hobby in availableHobbies" :key="hobby" class="checkbox-label">
              <input type="checkbox" :value="hobby" v-model="user.hobbies"> {{ hobby }}
            </label>
          </div>
        </div>

        <div class="control-group">
          <label>活躍度：</label>
          <input v-model.number="user.activityLevel" type="range" min="0" max="100" class="range-input">
          <span>{{ user.activityLevel }}%</span>
        </div>
      </div>
    </div>

    <div class="demo-section">
      <h3>🔍 監控設定</h3>
      <div class="watch-controls">
        <div class="control-group">
          <label class="checkbox-label">
            <input type="checkbox" v-model="watchSettings.enableNameWatch">
            監控用戶名變化
          </label>
        </div>

        <div class="control-group">
          <label class="checkbox-label">
            <input type="checkbox" v-model="watchSettings.enableDeepWatch">
            深度監控用戶對象
          </label>
        </div>

        <div class="control-group">
          <label class="checkbox-label">
            <input type="checkbox" v-model="watchSettings.enableActivityWatch">
            監控活躍度變化
          </label>
        </div>

        <div class="control-group">
          <button @click="clearLogs" class="btn btn-secondary">清除日誌</button>
          <button @click="stopAllWatchers" class="btn btn-warning">停止所有監控</button>
          <button @click="startAllWatchers" class="btn btn-primary">重新開始監控</button>
        </div>
      </div>
    </div>

    <div class="demo-section">
      <h3>📈 統計資訊</h3>
      <div class="stats-grid">
        <div class="stat-card">
          <h4>總變化次數</h4>
          <p class="stat-number">{{ totalChanges }}</p>
        </div>

        <div class="stat-card">
          <h4>用戶名長度</h4>
          <p class="stat-number">{{ user.name.length }}</p>
        </div>

        <div class="stat-card">
          <h4>興趣數量</h4>
          <p class="stat-number">{{ user.hobbies.length }}</p>
        </div>

        <div class="stat-card">
          <h4>用戶等級</h4>
          <p class="stat-number">{{ userLevel }}</p>
        </div>
      </div>
    </div>

    <div class="demo-section">
      <h3>📝 監控日誌</h3>
      <div class="logs-container">
        <div v-if="logs.length === 0" class="no-logs">
          暫無監控日誌，請修改上方的用戶資料來觸發監控
        </div>

        <div v-else class="log-list">
          <div v-for="(log, index) in logs" :key="index" class="log-entry" :class="log.type">
            <span class="log-time">{{ log.time }}</span>
            <span class="log-type">{{ log.type }}</span>
            <span class="log-message">{{ log.message }}</span>
          </div>
        </div>
      </div>
    </div>

    <div class="hint-section">
      <h4>💡 提示與參考</h4>
      <details>
        <summary>點擊查看實作提示</summary>
        <pre><code>// 基本 watch 用法
watch(user.name, (newValue, oldValue) => {
  console.log(`用戶名從 ${oldValue} 變為 ${newValue}`)
})

// 監控 ref
const count = ref(0)
watch(count, (newCount) => {
  console.log('計數變化:', newCount)
})

// 監控 reactive 對象的屬性
watch(() => user.age, (newAge, oldAge) => {
  console.log(`年齡從 ${oldAge} 變為 ${newAge}`)
})

// 深度監控
watch(user, (newUser, oldUser) => {
  console.log('用戶對象發生變化')
}, { deep: true })

// 監控多個數據源
watch([user.name, user.age], ([newName, newAge], [oldName, oldAge]) => {
  console.log('用戶名或年齡發生變化')
})

// watchEffect 自動追蹤依賴
watchEffect(() => {
  console.log(`用戶 ${user.name} 的活躍度是 ${user.activityLevel}%`)
})

// 停止監控
const stopWatcher = watch(user.name, callback)
// 調用 stopWatcher() 來停止監控

// 條件性監控
watch(user.activityLevel, (level) => {
  if (level > 80) {
    console.log('用戶非常活躍！')
  }
}, {
  immediate: true,  // 立即執行一次
  flush: 'post'     // 在組件更新後執行
})</code></pre>
      </details>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive, computed, watch, watchEffect, onUnmounted } from 'vue'

// 用戶數據
const user = reactive({
  name: '',
  age: 0,
  hobbies: [],
  activityLevel: 50
})

// 可選興趣
const availableHobbies = ['閱讀', '運動', '音樂', '旅行', '遊戲', '攝影']

// 監控設定
const watchSettings = reactive({
  enableNameWatch: true,
  enableDeepWatch: true,
  enableActivityWatch: true
})

// 日誌系統
const logs = ref([])
const totalChanges = ref(0)

// 監控器引用（用於停止監控）
const watchers = ref([])

// TODO: 完成以下功能

// 1. 計算用戶等級（基於年齡和活躍度）
const userLevel = computed(() => {
  // 請在這裡完成用戶等級計算邏輯
  return 'Bronze'
})

// 2. 添加日誌的輔助函數
const addLog = (type, message) => {
  // 請在這裡完成日誌添加邏輯

}

// 3. 監控用戶名變化
const watchUserName = () => {
  // 請在這裡使用 watch 監控 user.name 的變化

}

// 4. 深度監控用戶對象
const watchUserDeep = () => {
  // 請在這裡使用 watch 深度監控整個 user 對象

}

// 5. 監控活躍度變化
const watchActivityLevel = () => {
  // 請在這裡監控 user.activityLevel 的變化
  // 當活躍度超過 80 時給出特殊提示

}

// 6. 使用 watchEffect 自動追蹤
const setupWatchEffect = () => {
  // 請在這裡使用 watchEffect 自動追蹤用戶數據變化

}

// 7. 監控多個數據源
const watchMultipleSources = () => {
  // 請在這裡同時監控用戶名和年齡的變化

}

// 8. 清除日誌
const clearLogs = () => {
  // 請在這裡完成清除日誌的邏輯

}

// 9. 停止所有監控
const stopAllWatchers = () => {
  // 請在這裡停止所有活躍的監控器

}

// 10. 重新開始監控
const startAllWatchers = () => {
  // 請在這裡重新啟動所有監控器

}

// 組件卸載時清理
onUnmounted(() => {
  // TODO: 清理所有監控器

})
</script>

<style scoped>
.self-challenge {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}



.challenge-section {
  background: #fff3e0;
  padding: 1.5rem;
  border-radius: 8px;
  margin: 2rem 0;
}

.task-list {
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
}

.task-item {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.5rem;
  background: white;
  border-radius: 4px;
}

.task-item input[type="checkbox"] {
  width: 18px;
  height: 18px;
}

.demo-section {
  margin: 2rem 0;
  padding: 1.5rem;
  border: 1px solid #ddd;
  border-radius: 8px;
  background: #fafafa;
}

.user-controls,
.watch-controls {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 1rem;
  margin: 1rem 0;
}

.control-group {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.control-group label {
  font-weight: bold;
  color: #333;
}

.form-input {
  padding: 0.5rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 0.9rem;
}

.range-input {
  width: 100%;
}

.hobby-list {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.checkbox-label {
  display: flex !important;
  align-items: center;
  gap: 0.5rem;
  font-weight: normal !important;
  cursor: pointer;
}

.checkbox-label input {
  width: auto !important;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
  margin: 1rem 0;
}

.stat-card {
  background: white;
  padding: 1rem;
  border-radius: 8px;
  text-align: center;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.stat-number {
  font-size: 1.5rem;
  font-weight: bold;
  color: #1976d2;
  margin: 0.5rem 0;
}

.logs-container {
  background: white;
  border-radius: 8px;
  border: 1px solid #ddd;
  max-height: 400px;
  overflow-y: auto;
}

.no-logs {
  padding: 2rem;
  text-align: center;
  color: #666;
}

.log-list {
  padding: 1rem;
}

.log-entry {
  display: flex;
  gap: 1rem;
  padding: 0.5rem;
  border-bottom: 1px solid #eee;
  font-family: monospace;
  font-size: 0.9rem;
}

.log-entry:last-child {
  border-bottom: none;
}

.log-entry.watch {
  background: #e3f2fd;
}

.log-entry.watchEffect {
  background: #f1f8e9;
}

.log-entry.deep {
  background: #fff3e0;
}

.log-entry.activity {
  background: #fff9c4;
}

.log-time {
  color: #666;
  min-width: 80px;
}

.log-type {
  color: #1976d2;
  font-weight: bold;
  min-width: 100px;
}

.log-message {
  color: #333;
  flex: 1;
}

.btn {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9rem;
  transition: background-color 0.2s;
  margin-right: 0.5rem;
}

.btn-primary {
  background: #1976d2;
  color: white;
}

.btn-secondary {
  background: #757575;
  color: white;
}

.btn-warning {
  background: #ff9800;
  color: white;
}

.btn:hover {
  opacity: 0.9;
}

.hint-section {
  background: #e8f5e8;
  padding: 1.5rem;
  border-radius: 8px;
  margin: 2rem 0;
}

details {
  margin-top: 1rem;
}

summary {
  cursor: pointer;
  font-weight: bold;
  padding: 0.5rem;
  background: #c8e6c9;
  border-radius: 4px;
}

pre {
  background: #2d3748;
  color: #e2e8f0;
  padding: 1rem;
  border-radius: 4px;
  overflow-x: auto;
  margin-top: 1rem;
}

.implementation-section {
  background: #f3e5f5;
  padding: 1.5rem;
  border-radius: 8px;
  margin: 2rem 0;
  border-left: 4px solid #9c27b0;
}

.implementation-intro {
  margin-bottom: 1.5rem;
  font-size: 1rem;
  color: #424242;
}

.implementation-list {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-bottom: 2rem;
}

.implementation-item {
  background: white;
  border-radius: 8px;
  padding: 1rem;
  border-left: 3px solid #e0e0e0;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  transition: all 0.2s ease;
}

.implementation-item:hover {
  border-left-color: #9c27b0;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.15);
}

.function-header {
  display: flex;
  align-items: center;
  gap: 0.8rem;
  margin-bottom: 0.5rem;
}

.function-number {
  background: #9c27b0;
  color: white;
  border-radius: 50%;
  width: 24px;
  height: 24px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.8rem;
  font-weight: bold;
}

.function-name {
  font-family: 'Courier New', monospace;
  font-weight: bold;
  color: #2e7d32;
  background: #e8f5e8;
  padding: 0.2rem 0.5rem;
  border-radius: 4px;
  flex: 1;
}

.difficulty {
  padding: 0.2rem 0.6rem;
  border-radius: 12px;
  font-size: 0.75rem;
  font-weight: bold;
  text-transform: uppercase;
}

.difficulty.easy {
  background: #c8e6c9;
  color: #2e7d32;
}

.difficulty.medium {
  background: #ffe0b2;
  color: #f57c00;
}

.difficulty.hard {
  background: #ffcdd2;
  color: #d32f2f;
}

.function-description {
  color: #424242;
  line-height: 1.5;
}

.function-description small {
  color: #757575;
  font-style: italic;
  display: block;
  margin-top: 0.3rem;
}

.implementation-tips {
  background: white;
  padding: 1rem;
  border-radius: 8px;
  border: 1px solid #e1bee7;
}

.implementation-tips h4 {
  margin: 0 0 1rem 0;
  color: #9c27b0;
}

.implementation-tips ul {
  margin: 0;
  padding-left: 1.5rem;
}

.implementation-tips li {
  margin-bottom: 0.5rem;
  line-height: 1.4;
}

.implementation-tips strong {
  color: #6a1b9a;
}

.spec-details {
  margin-top: 0.5rem;
  padding: 0.8rem;
  border: 1px solid #e0e0e0;
  border-radius: 4px;
  background: #fafafa;
  font-size: 0.9rem;
}

.spec-details strong {
  font-weight: bold;
  color: #333;
}

.spec-details ul {
  margin: 0.5rem 0 0 0;
  padding-left: 1.2rem;
}

.spec-details li {
  margin-bottom: 0.4rem;
  line-height: 1.4;
}

.spec-details ul ul {
  margin-top: 0.3rem;
  padding-left: 1rem;
}

.spec-details ul ul li {
  margin-bottom: 0.2rem;
  font-size: 0.85rem;
}

.log-entry.activity {
  background: #fff9c4;
}
</style>
