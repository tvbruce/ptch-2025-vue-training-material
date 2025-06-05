<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - v-for 列表渲染</h2>
    <p class="route-info">📍 路徑：/ListSamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>挑戰任務：</strong>建立一個學生成績管理系統，練習各種 v-for 渲染技巧
    </p>

    <div class="challenge-section">
      <h3>🎯 挑戰清單</h3>
      <div class="task-list">
        <div class="task-item">
          <input type="checkbox" id="task1">
          <label for="task1">1. 使用 v-for 渲染學生列表</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task2">
          <label for="task2">2. 實作新增學生功能</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task3">
          <label for="task3">3. 實作刪除學生功能</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task4">
          <label for="task4">4. 實作編輯學生功能</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task5">
          <label for="task5">5. 計算平均分數</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task6">
          <label for="task6">6. 建立完整的學生成績管理系統</label>
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
            <span class="function-name">filteredUsers (computed)</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            根據搜尋條件篩選用戶列表
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>篩選條件：</strong>根據 searchTerm.value 搜尋姓名或email</li>
                <li><strong>大小寫：</strong>不區分大小寫搜尋</li>
                <li><strong>返回值：</strong>Array - 符合條件的用戶陣列</li>
                <li><strong>空搜尋：</strong>searchTerm 為空時返回所有用戶</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>使用 v-for 渲染動態列表</li>
                <li>實作列表項目的增刪改查</li>
                <li>處理空列表狀態顯示</li>
                <li>實作列表搜尋和篩選功能</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">2.</span>
            <span class="function-name">sortedUsers (computed)</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            根據選擇的排序方式對用戶進行排序
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>排序欄位：</strong>name, age, email, joinDate</li>
                <li><strong>排序方向：</strong>asc (升序) 或 desc (降序)</li>
                <li><strong>字串排序：</strong>使用 localeCompare 進行本地化排序</li>
                <li><strong>數字排序：</strong>直接比較數值大小</li>
                <li><strong>日期排序：</strong>轉換為時間戳進行比較</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作動態 key 綁定優化渲染</li>
                <li>處理列表項目的唯一標識</li>
                <li>實作列表排序功能</li>
                <li>優化大量資料的渲染性能</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">3.</span>
            <span class="function-name">addUser(userData)</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            新增用戶到列表中
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>參數：</strong>userData (object) - 包含用戶資訊的物件</li>
                <li><strong>必要欄位：</strong>name, email, age</li>
                <li><strong>ID 生成：</strong>自動生成唯一的用戶 ID</li>
                <li><strong>驗證：</strong>檢查 email 格式和必要欄位</li>
                <li><strong>重複檢查：</strong>避免相同 email 的用戶重複新增</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作列表項目的條件渲染</li>
                <li>根據狀態顯示不同的列表內容</li>
                <li>處理載入和錯誤狀態</li>
                <li>實作分頁或虛擬滾動</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">4.</span>
            <span class="function-name">removeUser(userId)</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            從列表中移除指定用戶
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>參數：</strong>userId (number) - 要移除的用戶 ID</li>
                <li><strong>移除方式：</strong>使用 filter 方法過濾掉指定用戶</li>
                <li><strong>確認機制：</strong>可以加入確認對話框</li>
                <li><strong>錯誤處理：</strong>用戶不存在時的處理</li>
              </ul>
            </div>
            <div class="task-requirements">
              <h5>🎯 實作任務：</h5>
              <ul>
                <li>實作嵌套列表的渲染</li>
                <li>處理多層級資料結構</li>
                <li>實作樹狀結構展開/收合</li>
                <li>優化嵌套渲染的性能</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">5.</span>
            <span class="function-name">addStudent()</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            新增學生到列表中
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>ID 生成：</strong>使用 Date.now() 或遞增數字生成唯一 ID</li>
                <li><strong>資料驗證：</strong>檢查姓名不為空，分數在 0-100 之間</li>
                <li><strong>新增操作：</strong>將新學生物件推入 students.value 陣列</li>
                <li><strong>表單重置：</strong>清空 newStudent 的所有欄位</li>
                <li><strong>物件格式：</strong>{ id, name, subject, score }</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">6.</span>
            <span class="function-name">deleteStudent(id)</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            根據 ID 刪除學生
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>參數：</strong>id (number) - 要刪除的學生 ID</li>
                <li><strong>篩選操作：</strong>使用 filter() 方法移除指定 ID 的學生</li>
                <li><strong>更新陣列：</strong>將篩選結果重新賦值給 students.value</li>
                <li><strong>確認機制：</strong>可選擇性加入刪除確認對話框</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">7.</span>
            <span class="function-name">editStudent(student)</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            開始編輯學生資料
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>參數：</strong>student (object) - 要編輯的學生物件</li>
                <li><strong>設定編輯：</strong>將 editingId.value 設為學生 ID</li>
                <li><strong>複製資料：</strong>將學生資料複製到 editForm.value</li>
                <li><strong>深拷貝：</strong>使用 {...student} 或 Object.assign() 避免直接引用</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">8.</span>
            <span class="function-name">saveEdit()</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            儲存編輯的學生資料
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>查找學生：</strong>在 students.value 中找到對應 ID 的學生</li>
                <li><strong>資料驗證：</strong>檢查編輯表單的資料有效性</li>
                <li><strong>更新資料：</strong>將 editForm.value 的資料更新到學生物件</li>
                <li><strong>重置狀態：</strong>清空 editingId.value 和 editForm.value</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">9.</span>
            <span class="function-name">cancelEdit()</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            取消編輯操作
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>重置編輯：</strong>將 editingId.value 設為 null</li>
                <li><strong>清空表單：</strong>重置 editForm.value 為空物件</li>
                <li><strong>恢復顯示：</strong>回到正常的列表顯示模式</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">10.</span>
            <span class="function-name">averageScore (computed)</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            計算所有學生的平均分數
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>計算邏輯：</strong>使用 reduce() 計算總分，除以學生數量</li>
                <li><strong>空陣列處理：</strong>當沒有學生時返回 0</li>
                <li><strong>格式化：</strong>使用 toFixed(1) 保留一位小數</li>
                <li><strong>返回類型：</strong>number - 平均分數</li>
              </ul>
            </div>
          </div>
        </div>
      </div>

      <div class="implementation-tips">
        <h4>💡 開發提示</h4>
        <ul>
          <li><strong>v-for 語法：</strong>記得使用 :key 綁定唯一識別符</li>
          <li><strong>陣列操作：</strong>push(), filter(), find(), map() 是常用方法</li>
          <li><strong>表單驗證：</strong>在操作前檢查資料的有效性</li>
          <li><strong>狀態管理：</strong>合理使用 ref 管理編輯狀態</li>
          <li><strong>深拷貝：</strong>編輯時避免直接修改原始資料</li>
        </ul>
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
@import '@/assets/self-challenge.css';

.self-challenge {
  max-width: 1200px;
  margin: 0 auto;
  padding: 2rem;
}

.practice-requirements {
  background: linear-gradient(135deg, #fff3e0 0%, #ffecb3 100%);
  padding: 2rem;
  border-radius: 12px;
  margin: 2rem 0;
  border-left: 4px solid #ff9800;
}

.requirement-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(450px, 1fr));
  gap: 1.5rem;
  margin-top: 1.5rem;
}

.requirement-card {
  background: white;
  padding: 1.5rem;
  border-radius: 8px;
  border: 1px solid #e0e0e0;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.requirement-card h4 {
  color: #d84315;
  margin-bottom: 0.5rem;
}

.requirement-card p {
  color: #666;
  margin-bottom: 1rem;
}

.specs h5 {
  color: #1976d2;
  margin: 1rem 0 0.5rem 0;
  font-size: 0.9rem;
}

.specs ul {
  margin: 0.5rem 0;
  padding-left: 1.5rem;
}

.specs li {
  margin: 0.3rem 0;
  color: #444;
}

.specs pre {
  background: #2d3748;
  color: #e2e8f0;
  padding: 1rem;
  border-radius: 4px;
  font-size: 0.85rem;
  margin: 0.5rem 0;
  overflow-x: auto;
}

.specs code {
  background: #f5f5f5;
  padding: 0.2rem 0.4rem;
  border-radius: 3px;
  font-size: 0.85rem;
  color: #d32f2f;
}
</style>
