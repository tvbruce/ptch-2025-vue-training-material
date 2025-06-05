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
            <span class="function-number">2.</span>
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
            <span class="function-number">3.</span>
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
            <span class="function-number">4.</span>
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
            <span class="function-number">5.</span>
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
            <span class="function-number">6.</span>
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

    <!-- 練習要求區塊 -->
    <div class="practice-requirements">
      <h3>📋 練習要求</h3>
      <div class="requirement-grid">
        <div class="requirement-card">
          <h4>🎯 任務一：列表渲染</h4>
          <p><strong>目標：</strong>使用 v-for 渲染學生列表</p>
          <div class="specs">
            <h5>規格說明：</h5>
            <ul>
              <li>遍歷 <code>students</code> 陣列</li>
              <li>使用 <code>student.id</code> 作為 key</li>
              <li>顯示學生姓名、科目、分數</li>
              <li>套用 <code>student-card</code> 樣式類別</li>
            </ul>
            <h5>邏輯說明：</h5>
            <pre><code>&lt;div v-for="student in students" :key="student.id" class="student-card"&gt;
  &lt;!-- 在這裡顯示學生資訊 --&gt;
&lt;/div&gt;</code></pre>
          </div>
        </div>

        <div class="requirement-card">
          <h4>🎯 任務二：新增學生功能</h4>
          <p><strong>目標：</strong>實作 addStudent 方法</p>
          <div class="specs">
            <h5>規格說明：</h5>
            <ul>
              <li>從表單獲取新學生資料</li>
              <li>生成新的 id（建議用時間戳或遞增數字）</li>
              <li>將新學生加入 students 陣列</li>
              <li>清空表單欄位</li>
            </ul>
            <h5>邏輯說明：</h5>
            <pre><code>const addStudent = () => {
  // 1. 生成新 id
  // 2. 建立新學生物件
  // 3. 加入陣列
  // 4. 重置表單
}</code></pre>
          </div>
        </div>

        <div class="requirement-card">
          <h4>🎯 任務三：刪除學生功能</h4>
          <p><strong>目標：</strong>實作 removeStudent 方法</p>
          <div class="specs">
            <h5>規格說明：</h5>
            <ul>
              <li>接收學生 id 作為參數</li>
              <li>從 students 陣列中移除對應學生</li>
              <li>在每個學生卡片加入刪除按鈕</li>
            </ul>
            <h5>邏輯說明：</h5>
            <pre><code>const removeStudent = (studentId) => {
  // 使用 filter 或 findIndex + splice 方法
  // 找到對應學生並移除
}</code></pre>
          </div>
        </div>

        <div class="requirement-card">
          <h4>🎯 任務四：成績篩選</h4>
          <p><strong>目標：</strong>實作 filteredStudents 計算屬性</p>
          <div class="specs">
            <h5>規格說明：</h5>
            <ul>
              <li>根據 showPassed 狀態篩選學生</li>
              <li>及格標準：分數 ≥ 60</li>
              <li>修改 v-for 使用 filteredStudents</li>
            </ul>
            <h5>邏輯說明：</h5>
            <pre><code>const filteredStudents = computed(() => {
  // 如果 showPassed 為 true，只返回及格學生
  // 否則返回全部學生
})</code></pre>
          </div>
        </div>

        <div class="requirement-card">
          <h4>🎯 任務五：成績樣式</h4>
          <p><strong>目標：</strong>根據成績顯示不同樣式</p>
          <div class="specs">
            <h5>規格說明：</h5>
            <ul>
              <li>及格學生：套用 <code>passed</code> 類別（綠色邊框）</li>
              <li>不及格學生：套用 <code>failed</code> 類別（紅色邊框）</li>
              <li>使用條件式 class 綁定</li>
            </ul>
            <h5>邏輯說明：</h5>
            <pre><code>:class="{
  'passed': student.score >= 60,
  'failed': student.score < 60
}"</code></pre>
          </div>
        </div>

        <div class="requirement-card">
          <h4>🎯 任務六：統計功能</h4>
          <p><strong>目標：</strong>實作統計相關的計算屬性</p>
          <div class="specs">
            <h5>規格說明：</h5>
            <ul>
              <li><code>totalStudents</code>：學生總數</li>
              <li><code>passedCount</code>：及格學生數量</li>
              <li><code>averageScore</code>：平均分數（保留一位小數）</li>
            </ul>
            <h5>邏輯說明：</h5>
            <pre><code>// 使用 computed 建立計算屬性
// 利用陣列方法如 length, filter, reduce</code></pre>
          </div>
        </div>
      </div>
    </div>

    <div class="demo-section">
      <h3>📋 學生成績列表</h3>
      <div class="controls">
        <button @click="sortByScore" class="btn btn-primary">按分數排序</button>
        <button @click="showPassed = !showPassed" class="btn btn-secondary">
          {{ showPassed ? '顯示全部' : '只顯示及格' }}
        </button>
      </div>

      <!-- 🎯 任務一：在這裡完成 v-for 渲染 -->
      <div class="student-grid">
        <!-- 請在這裡使用 v-for 渲染學生列表 -->
      </div>
    </div>

    <div class="demo-section">
      <h3>➕ 新增學生</h3>
      <div class="add-form">
        <input v-model="newStudent.name" placeholder="學生姓名" class="form-input">
        <input v-model="newStudent.subject" placeholder="科目" class="form-input">
        <input v-model.number="newStudent.score" type="number" placeholder="分數" class="form-input">
        <!-- 🎯 任務二：完成 addStudent 方法 -->
        <button @click="addStudent" class="btn btn-success">新增學生</button>
      </div>
    </div>

    <div class="stats-section">
      <h3>📊 統計資料</h3>
      <div class="stats-grid">
        <div class="stat-card">
          <h4>總學生數</h4>
          <!-- 🎯 任務六：顯示學生總數 -->
          <p class="stat-number">{{ totalStudents }}</p>
        </div>
        <div class="stat-card">
          <h4>及格人數</h4>
          <!-- 🎯 任務六：計算及格學生數量 -->
          <p class="stat-number">{{ passedCount }}</p>
        </div>
        <div class="stat-card">
          <h4>平均分數</h4>
          <!-- 🎯 任務六：計算平均分數 -->
          <p class="stat-number">{{ averageScore }}</p>
        </div>
      </div>
    </div>

    <div class="hint-section">
      <h4>💡 開發提示</h4>
      <details>
        <summary>點擊查看開發提示</summary>
        <div class="hints">
          <h5>常用語法參考：</h5>
          <pre><code>// v-for 基本語法
&lt;div v-for="item in items" :key="item.id"&gt;

// 條件式 class
:class="{ 'className': condition }"

// 事件處理
@click="methodName"
@click="methodName(parameter)"

// 計算屬性
const computed屬性名 = computed(() => {
  return 計算邏輯
})

// 陣列常用方法
array.push(item)           // 新增
array.filter(條件函數)      // 篩選
array.reduce(累加函數, 初值) // 累加計算</code></pre>

          <h5>除錯建議：</h5>
          <ul>
            <li>使用 console.log() 檢查資料狀態</li>
            <li>在 Vue DevTools 中觀察響應式資料變化</li>
            <li>確認 key 屬性的唯一性</li>
            <li>檢查方法是否正確綁定到按鈕事件</li>
          </ul>
        </div>
      </details>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 學生資料（已提供初始資料）
const students = ref([
  { id: 1, name: '小明', subject: '數學', score: 85 },
  { id: 2, name: '小華', subject: '英文', score: 92 },
  { id: 3, name: '小美', subject: '數學', score: 45 },
  { id: 4, name: '小強', subject: '物理', score: 78 },
  { id: 5, name: '小芳', subject: '化學', score: 55 }
])

// 新學生表單資料
const newStudent = ref({
  name: '',
  subject: '',
  score: 0
})

// 控制顯示狀態
const showPassed = ref(false)

// 🎯 任務四：實作 filteredStudents 計算屬性
// 提示：根據 showPassed 的值來篩選學生
const filteredStudents = computed(() => {
  // 請在這裡完成篩選邏輯
  // 如果 showPassed 為 true，只返回及格學生（score >= 60）
  // 否則返回全部學生
  return students.value // 暫時返回全部學生，待學員實作
})

// 🎯 任務二：實作 addStudent 方法
const addStudent = () => {
  // 請在這裡完成新增學生的邏輯
  // 1. 驗證表單資料是否完整
  // 2. 生成新的 id
  // 3. 建立新學生物件
  // 4. 加入 students 陣列
  // 5. 重置表單
}

// 🎯 任務三：實作 removeStudent 方法
const removeStudent = (studentId) => {
  // 請在這裡完成刪除學生的邏輯
  // 提示：可以使用 filter 方法或 findIndex + splice
  console.log('待刪除學生ID:', studentId) // 暫時輸出，待學員實作
}

// 排序功能（已提供）
const sortByScore = () => {
  students.value.sort((a, b) => b.score - a.score)
}

// 🎯 任務六：實作統計相關的計算屬性
const totalStudents = computed(() => {
  // 請在這裡完成總數計算
  return 0 // 暫時返回 0，待學員實作
})

const passedCount = computed(() => {
  // 請在這裡完成及格人數計算
  // 提示：使用 filter 方法篩選 score >= 60 的學生
  return 0 // 暫時返回 0，待學員實作
})

const averageScore = computed(() => {
  // 請在這裡完成平均分數計算
  // 提示：使用 reduce 方法計算總分，再除以學生數量
  // 可以使用 toFixed(1) 保留一位小數
  return 0 // 暫時返回 0，待學員實作
})
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

.demo-section {
  margin: 2rem 0;
  padding: 1.5rem;
  border: 1px solid #ddd;
  border-radius: 8px;
  background: #fafafa;
}

.controls {
  display: flex;
  gap: 1rem;
  margin-bottom: 1rem;
}

.student-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 1rem;
  margin: 1rem 0;
  min-height: 100px;
  border: 2px dashed #ccc;
  padding: 1rem;
  border-radius: 8px;
  background: #f9f9f9;
  position: relative;
}

.student-grid:empty::after {
  content: "🎯 請在這裡完成 v-for 渲染學生列表";
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  color: #666;
  font-size: 1.1rem;
}

.student-card {
  background: white;
  padding: 1rem;
  border-radius: 8px;
  border: 1px solid #ddd;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.student-card.passed {
  border-left: 4px solid #4caf50;
}

.student-card.failed {
  border-left: 4px solid #f44336;
}

.add-form {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  align-items: center;
}

.form-input {
  padding: 0.5rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  min-width: 150px;
}

.stats-section {
  background: #f1f8e9;
  padding: 1.5rem;
  border-radius: 8px;
  margin: 2rem 0;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 1rem;
  margin-top: 1rem;
}

.stat-card {
  background: white;
  padding: 1rem;
  border-radius: 8px;
  text-align: center;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.stat-number {
  font-size: 2rem;
  font-weight: bold;
  color: #1976d2;
  margin: 0.5rem 0;
}

.btn {
  padding: 0.5rem 1rem;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 0.9rem;
  transition: background-color 0.2s;
}

.btn-primary {
  background: #1976d2;
  color: white;
}

.btn-secondary {
  background: #757575;
  color: white;
}

.btn-success {
  background: #4caf50;
  color: white;
}

.btn-danger {
  background: #f44336;
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

.hints {
  margin-top: 1rem;
}

.hints h5 {
  color: #2e7d32;
  margin: 1rem 0 0.5rem 0;
}

.hints pre {
  background: #2d3748;
  color: #e2e8f0;
  padding: 1rem;
  border-radius: 4px;
  overflow-x: auto;
  margin: 0.5rem 0;
}

.hints ul {
  margin: 0.5rem 0;
  padding-left: 1.5rem;
}

.hints li {
  margin: 0.3rem 0;
  color: #444;
}
</style>
