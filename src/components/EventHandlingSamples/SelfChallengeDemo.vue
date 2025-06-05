<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - Event 事件處理</h2>
    <p class="route-info">📍 路徑：/EventHandlingSamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>挑戰任務：</strong>建立一個簡單的互動計數器，練習各種事件處理技巧
    </p>

    <div class="challenge-section">
      <h3>🎯 挑戰清單</h3>
      <div class="task-list">
        <div class="task-item">
          <input type="checkbox" id="task1">
          <label for="task1">1. 實作基本點擊事件（增加、減少、重置）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task2">
          <label for="task2">2. 實作鍵盤事件處理（Space、r、-鍵）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task3">
          <label for="task3">3. 實作滑鼠事件（hover、雙擊）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task4">
          <label for="task4">4. 使用事件修飾符（prevent、stop、once）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task5">
          <label for="task5">5. 實作表單事件處理（submit、input）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task6">
          <label for="task6">6. 建立完整的互動計數器系統</label>
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
            <span class="function-name">increment()</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            增加計數器的值
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>操作：</strong>將 count.value 增加 1</li>
                <li><strong>限制：</strong>最大值不超過 100</li>
                <li><strong>日誌：</strong>記錄操作到 actionHistory 陣列</li>
                <li><strong>格式：</strong>{ action: 'increment', value: count.value, time: new Date().toLocaleTimeString()
                  }</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作「增加」按鈕的點擊事件</li>
                <li>實作「減少」按鈕的點擊事件</li>
                <li>實作「重置」按鈕的點擊事件</li>
                <li>使用 @click 事件綁定函數</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">2.</span>
            <span class="function-name">decrement()</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            減少計數器的值
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>操作：</strong>將 count.value 減少 1</li>
                <li><strong>限制：</strong>最小值不低於 0</li>
                <li><strong>日誌：</strong>記錄操作到 actionHistory 陣列</li>
                <li><strong>格式：</strong>{ action: 'decrement', value: count.value, time: new Date().toLocaleTimeString()
                  }</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>按下 Space 鍵增加計數</li>
                <li>按下 r 或 R 鍵重置計數</li>
                <li>按下 - 鍵減少計數</li>
                <li>使用全域 keydown 事件監聽器</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">3.</span>
            <span class="function-name">reset()</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            重置計數器為 0
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>操作：</strong>將 count.value 設為 0</li>
                <li><strong>清理：</strong>清空 actionHistory 陣列</li>
                <li><strong>日誌：</strong>記錄重置操作</li>
                <li><strong>格式：</strong>{ action: 'reset', value: 0, time: new Date().toLocaleTimeString() }</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>滑鼠進入計數顯示區域時變色</li>
                <li>滑鼠離開時恢復原色</li>
                <li>追蹤滑鼠在區域內的位置</li>
                <li>使用 @mouseenter、@mouseleave、@mousemove</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">4.</span>
            <span class="function-name">handleKeydown(event)</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            處理鍵盤按鍵事件
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>Space 鍵：</strong>調用 increment() 函數</li>
                <li><strong>r 或 R 鍵：</strong>調用 reset() 函數</li>
                <li><strong>- 鍵：</strong>調用 decrement() 函數</li>
                <li><strong>事件處理：</strong>使用 event.key 判斷按鍵</li>
                <li><strong>防止預設：</strong>對處理的按鍵調用 event.preventDefault()</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>表單提交時阻止頁面刷新</li>
                <li>雙擊時阻止文字選取</li>
                <li>右鍵選單時顯示自訂選單</li>
                <li>使用 .prevent、.stop 等修飾符</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">5.</span>
            <span class="function-name">handleDoubleClick()</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            處理雙擊事件，快速增加計數
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>操作：</strong>一次增加 5</li>
                <li><strong>限制：</strong>檢查不超過最大值 100</li>
                <li><strong>日誌：</strong>記錄為 'double-click' 操作</li>
                <li><strong>視覺回饋：</strong>設定 isDoubleClicked.value = true，1秒後重置為 false</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>設定步進值的表單驗證</li>
                <li>處理表單提交事件</li>
                <li>實作輸入值的範圍檢查</li>
                <li>使用事件修飾符阻止預設行為</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">6.</span>
            <span class="function-name">handleSubmit(event)</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            處理表單提交事件
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>防止預設：</strong>調用 event.preventDefault() 阻止表單提交</li>
                <li><strong>驗證：</strong>檢查 targetValue.value 是否為有效數字（0-100）</li>
                <li><strong>設定：</strong>如果有效，將 count.value 設為 targetValue.value</li>
                <li><strong>清空：</strong>重置 targetValue.value 為空字串</li>
                <li><strong>日誌：</strong>記錄為 'set-target' 操作</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>整合所有事件處理功能</li>
                <li>實作視覺回饋和動畫效果</li>
                <li>建立完整的使用者互動體驗</li>
                <li>處理邊界條件和錯誤狀態</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">7.</span>
            <span class="function-name">生命週期設定</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            設定全域鍵盤事件監聽器
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>onMounted：</strong>添加 'keydown' 事件監聽器到 document</li>
                <li><strong>onUnmounted：</strong>移除 'keydown' 事件監聽器</li>
                <li><strong>監聽器：</strong>綁定 handleKeydown 函數</li>
                <li><strong>清理：</strong>確保組件卸載時正確清理事件監聽器</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>在 onMounted 中添加事件監聽器</li>
                <li>在 onUnmounted 中清理事件監聽器</li>
                <li>確保不會造成記憶體洩漏</li>
                <li>處理多個生命週期鉤子</li>
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
            <pre><code>// 基本事件綁定
&lt;button @click="handleClick"&gt;點擊&lt;/button&gt;
&lt;input @keyup.enter="handleEnter"&gt;

// 事件修飾符
&lt;form @submit.prevent="handleSubmit"&gt;  // 阻止預設行為
&lt;div @click.stop="handleClick"&gt;       // 阻止事件冒泡
&lt;div @contextmenu.prevent="showMenu"&gt; // 阻止右鍵選單

// 鍵盤事件
&lt;input @keydown="handleKeydown"&gt;
&lt;input @keyup.space="handleSpace"&gt;
&lt;input @keyup.enter="handleEnter"&gt;

// 滑鼠事件
&lt;div @mouseenter="handleMouseEnter"&gt;
&lt;div @mouseleave="handleMouseLeave"&gt;
&lt;div @mousemove="handleMouseMove"&gt;

// 事件物件使用
const handleKeydown = (event) => {
  console.log(event.key)      // 按鍵名稱
  console.log(event.target)   // 觸發元素
}

// 全域事件監聽
onMounted(() => {
  window.addEventListener('keydown', handleGlobalKeydown)
})

onUnmounted(() => {
  window.removeEventListener('keydown', handleGlobalKeydown)
})</code></pre>

            <h5>重要概念：</h5>
            <ul>
              <li><strong>事件物件：</strong>使用 event.key 獲取按鍵名稱</li>
              <li><strong>事件修飾符：</strong>可以使用 @click.prevent、@submit.prevent 等</li>
              <li><strong>數值驗證：</strong>使用 Number() 轉換和 isNaN() 檢查</li>
              <li><strong>定時器：</strong>使用 setTimeout 實現延遲效果</li>
              <li><strong>事件清理：</strong>記得在 onUnmounted 中移除事件監聽器</li>
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
