<template>
  <div class="self-challenge">
    <h2>🎯 自我試煉 - 屬性綁定</h2>
    <p class="route-info">📍 路徑：/AttributeBindingSamples/SelfChallengeDemo.vue</p>
    <p class="description">
      📝 <strong>挑戰任務：</strong>建立一個動態卡片組件，練習各種屬性綁定技巧
    </p>

    <div class="challenge-section">
      <h3>🎯 挑戰清單</h3>
      <div class="task-list">
        <div class="task-item">
          <input type="checkbox" id="task1">
          <label for="task1">1. 使用 v-bind 綁定基本屬性（src、alt、href）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task2">
          <label for="task2">2. 實作動態 Class 綁定（物件語法、陣列語法）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task3">
          <label for="task3">3. 實作動態 Style 綁定（內聯樣式控制）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task4">
          <label for="task4">4. 實作條件屬性綁定（disabled、required）</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task5">
          <label for="task5">5. 使用 v-bind 物件語法批量綁定屬性</label>
        </div>
        <div class="task-item">
          <input type="checkbox" id="task6">
          <label for="task6">6. 建立完整的動態卡片組件</label>
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
            <span class="function-name">cardImageSrc (computed)</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            根據選擇的主題返回對應的圖片路徑
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>參數：</strong>使用 selectedTheme.value 作為判斷條件</li>
                <li><strong>主題對應：</strong>
                  <ul>
                    <li>'nature' → '/images/nature.jpg'</li>
                    <li>'technology' → '/images/tech.jpg'</li>
                    <li>'art' → '/images/art.jpg'</li>
                    <li>預設 → '/images/default.jpg'</li>
                  </ul>
                </li>
                <li><strong>返回值：</strong>string - 圖片檔案路徑</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">2.</span>
            <span class="function-name">cardClasses (computed)</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            根據卡片狀態計算動態 CSS 類別
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>基礎類別：</strong>總是包含 'dynamic-card'</li>
                <li><strong>主題類別：</strong>`theme-${selectedTheme.value}`</li>
                <li><strong>狀態類別：</strong>
                  <ul>
                    <li>isActive.value → 'active'</li>
                    <li>isHighlighted.value → 'highlighted'</li>
                    <li>isLoading.value → 'loading'</li>
                  </ul>
                </li>
                <li><strong>返回格式：</strong>物件語法 { 'class-name': boolean }</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">3.</span>
            <span class="function-name">cardStyles (computed)</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            根據使用者設定計算動態內聯樣式
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>背景顏色：</strong>backgroundColor: customColor.value</li>
                <li><strong>邊框寬度：</strong>borderWidth: `${borderWidth.value}px`</li>
                <li><strong>透明度：</strong>opacity: opacity.value / 100</li>
                <li><strong>變換效果：</strong>transform: `scale(${scale.value})`</li>
                <li><strong>返回格式：</strong>物件包含所有樣式屬性</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">4.</span>
            <span class="function-name">linkAttributes (computed)</span>
            <span class="difficulty medium">中等</span>
          </div>
          <div class="function-description">
            計算連結的動態屬性物件
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>href：</strong>linkUrl.value 或 '#'</li>
                <li><strong>target：</strong>openInNewTab.value ? '_blank' : '_self'</li>
                <li><strong>rel：</strong>openInNewTab.value ? 'noopener noreferrer' : undefined</li>
                <li><strong>title：</strong>linkTitle.value</li>
                <li><strong>注意：</strong>undefined 的屬性不應該出現在返回物件中</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">5.</span>
            <span class="function-name">formFieldAttrs (computed)</span>
            <span class="difficulty hard">困難</span>
          </div>
          <div class="function-description">
            為表單欄位計算條件屬性
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>disabled：</strong>isFormDisabled.value</li>
                <li><strong>required：</strong>isRequired.value</li>
                <li><strong>placeholder：</strong>placeholderText.value</li>
                <li><strong>maxlength：</strong>maxLength.value > 0 ? maxLength.value : undefined</li>
                <li><strong>pattern：</strong>validationPattern.value || undefined</li>
                <li><strong>條件邏輯：</strong>只有在條件為 true 時才包含該屬性</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="implementation-item">
          <div class="function-header">
            <span class="function-number">6.</span>
            <span class="function-name">resetCardSettings()</span>
            <span class="difficulty easy">簡單</span>
          </div>
          <div class="function-description">
            重置所有卡片設定為預設值
            <div class="spec-details">
              <strong>📋 詳細規格：</strong>
              <ul>
                <li><strong>主題：</strong>selectedTheme.value = 'nature'</li>
                <li><strong>狀態：</strong>isActive, isHighlighted, isLoading 都設為 false</li>
                <li><strong>樣式：</strong>customColor = '#ffffff', borderWidth = 2, opacity = 100, scale = 1</li>
                <li><strong>連結：</strong>清空 linkUrl, linkTitle, openInNewTab = false</li>
                <li><strong>表單：</strong>重置所有表單相關設定</li>
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
            <pre><code>// 基本屬性綁定
&lt;img :src="imageUrl" :alt="imageAlt"&gt;
&lt;a :href="linkUrl" :target="isExternal ? '_blank' : '_self'"&gt;

// Class 綁定（物件語法）
:class="{
  active: isActive,
  'has-error': hasError,
  highlighted: isHighlighted
}"

// Class 綁定（陣列語法）
:class="[baseClass, sizeClass, { active: isActive }]"

// Style 綁定
:style="{
  color: textColor,
  fontSize: fontSize + 'px',
  backgroundColor: bgColor
}"

// 條件屬性綁定
&lt;button :disabled="!isValid" :title="tooltip"&gt;</code></pre>

            <h5>重要概念：</h5>
            <ul>
              <li><strong>v-bind 簡寫：</strong>可以使用 : 作為 v-bind 的簡寫形式</li>
              <li><strong>Class 綁定：</strong>可以混合使用字串、陣列、物件語法</li>
              <li><strong>Style 綁定：</strong>注意 CSS 屬性名稱的 camelCase 轉換</li>
              <li><strong>條件屬性：</strong>使用三元運算子或邏輯運算子處理條件</li>
              <li><strong>物件語法：</strong>v-bind 可以接受物件來批量綁定多個屬性</li>
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
          <h4>🎯 任務一：基礎屬性綁定</h4>
          <p><strong>目標：</strong>使用 v-bind 綁定基本屬性</p>
          <div class="specs">
            <h5>規格說明：</h5>
            <ul>
              <li>綁定圖片的 src 和 alt 屬性</li>
              <li>綁定連結的 href 和 target 屬性</li>
              <li>使用簡寫語法 (:)</li>
              <li>處理空值的情況</li>
            </ul>
          </div>
        </div>

        <div class="requirement-card">
          <h4>🎯 任務二：動態 Class 綁定</h4>
          <p><strong>目標：</strong>實作動態樣式切換</p>
          <div class="specs">
            <h5>規格說明：</h5>
            <ul>
              <li>使用物件語法控制多個 CSS 類別</li>
              <li>使用陣列語法組合樣式</li>
              <li>實作主題切換功能</li>
              <li>根據狀態顯示不同樣式</li>
            </ul>
          </div>
        </div>

        <div class="requirement-card">
          <h4>🎯 任務三：Style 屬性綁定</h4>
          <p><strong>目標：</strong>動態控制元素樣式</p>
          <div class="specs">
            <h5>規格說明：</h5>
            <ul>
              <li>使用物件語法設定內聯樣式</li>
              <li>綁定顏色、尺寸、位置等屬性</li>
              <li>實作即時預覽功能</li>
              <li>使用 CSS 變數控制主題</li>
            </ul>
          </div>
        </div>

        <div class="requirement-card">
          <h4>🎯 任務四：條件屬性綁定</h4>
          <p><strong>目標：</strong>根據條件動態添加屬性</p>
          <div class="specs">
            <h5>規格說明：</h5>
            <ul>
              <li>實作表單驗證狀態</li>
              <li>動態禁用/啟用元素</li>
              <li>條件性顯示提示信息</li>
              <li>多屬性物件綁定</li>
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

      <!-- 任務一：基礎屬性綁定 -->
      <div class="task-section">
        <h4>任務一：基礎屬性綁定實作</h4>
        <div class="controls">
          <input v-model="cardData.imageUrl" placeholder="輸入圖片網址" class="input-field">
          <input v-model="cardData.title" placeholder="輸入卡片標題" class="input-field">
          <input v-model="cardData.linkUrl" placeholder="輸入連結網址" class="input-field">
        </div>

        <div class="practice-area">
          <div class="card-preview">
            <!-- TODO: 學員需要在這裡實作屬性綁定 -->
            <img src="" alt="" class="card-image">
            <h4>標題顯示區</h4>
            <a href="#" target="" class="card-link">查看詳情</a>

            <!-- 提示：需要綁定的屬性
            - img 的 src 綁定到 cardData.imageUrl (為空時使用 defaultImage)
            - img 的 alt 綁定到 cardData.title + '的圖片'
            - h4 的內容顯示 cardData.title (為空時顯示 '(未設定標題)')
            - a 的 href 綁定到 cardData.linkUrl (為空時使用 '#')
            - a 的 target 在有 linkUrl 時設為 '_blank'
            -->
          </div>
        </div>
      </div>

      <!-- 任務二：動態 Class 綁定 -->
      <div class="task-section">
        <h4>任務二：動態 Class 綁定實作</h4>
        <div class="controls">
          <label class="checkbox-label">
            <input type="checkbox" v-model="cardState.isActive">
            啟用狀態 (active)
          </label>
          <label class="checkbox-label">
            <input type="checkbox" v-model="cardState.isHighlighted">
            高亮顯示 (highlighted)
          </label>
          <label class="checkbox-label">
            <input type="checkbox" v-model="cardState.hasError">
            錯誤狀態 (error)
          </label>
          <select v-model="cardState.size" class="select-field">
            <option value="small">小尺寸</option>
            <option value="medium">中尺寸</option>
            <option value="large">大尺寸</option>
          </select>
        </div>

        <div class="practice-area">
          <div class="dynamic-card">
            <!-- TODO: 學員需要在這裡實作動態 Class 綁定 -->
            <div class="status-card">
              <h4>動態樣式卡片</h4>
              <p>這個卡片會根據狀態改變樣式</p>

              <!-- 提示：需要實作的 class 綁定
              - 使用物件語法綁定 active, highlighted, error 狀態
              - 使用計算屬性結合 size 狀態 (size-small, size-medium, size-large)
              - 當 isActive 且 isHighlighted 時添加 'featured' class
              -->
            </div>

            <div class="class-info">
              <p>當前 Classes: <code>{{ getCurrentClasses() }}</code></p>
            </div>
          </div>
        </div>
      </div>

      <!-- 任務三：Style 屬性綁定 -->
      <div class="task-section">
        <h4>任務三：Style 屬性綁定實作</h4>
        <div class="controls">
          <input v-model="styleControls.backgroundColor" type="color" class="color-input">
          <label>背景顏色</label>

          <input v-model="styleControls.textColor" type="color" class="color-input">
          <label>文字顏色</label>

          <input v-model.number="styleControls.fontSize" type="range" min="12" max="24" class="range-input">
          <label>字體大小: {{ styleControls.fontSize }}px</label>

          <input v-model.number="styleControls.padding" type="range" min="10" max="40" class="range-input">
          <label>內距: {{ styleControls.padding }}px</label>

          <input v-model.number="styleControls.borderRadius" type="range" min="0" max="20" class="range-input">
          <label>圓角: {{ styleControls.borderRadius }}px</label>
        </div>

        <div class="practice-area">
          <div class="style-preview">
            <!-- TODO: 學員需要在這裡實作 Style 綁定 -->
            <div class="styleable-box">
              <h4>自定義樣式預覽</h4>
              <p>調整上方控制項來改變我的樣式！</p>

              <!-- 提示：需要實作的 style 綁定
              - 使用物件語法綁定背景色、文字色、字體大小、內距、圓角
              - 使用計算屬性組合所有樣式
              - 添加過渡效果 transition: 'all 0.3s ease'
              -->
            </div>
          </div>
        </div>
      </div>

      <!-- 任務四：條件屬性綁定 -->
      <div class="task-section">
        <h4>任務四：條件屬性綁定實作</h4>
        <div class="controls">
          <input v-model="formData.username" placeholder="用戶名稱" class="input-field">
          <input v-model="formData.email" placeholder="電子郵件" class="input-field">
          <input v-model="formData.website" placeholder="個人網站" class="input-field">

          <label class="checkbox-label">
            <input type="checkbox" v-model="formData.isPublic">
            公開資料
          </label>
          <label class="checkbox-label">
            <input type="checkbox" v-model="formData.newsletter">
            訂閱電子報
          </label>
        </div>

        <div class="practice-area">
          <div class="user-profile">
            <!-- TODO: 學員需要在這裡實作條件屬性綁定 -->
            <div class="profile-card">
              <h4>用戶資料預覽</h4>

              <div class="profile-field">
                <label>用戶名：</label>
                <span>{{ formData.username || '(未填寫)' }}</span>
                <!-- 提示：根據 username 長度添加驗證狀態 class -->
              </div>

              <div class="profile-field">
                <label>Email：</label>
                <span>{{ formData.email || '(未填寫)' }}</span>
                <!-- 提示：根據 email 格式添加驗證狀態 class -->
              </div>

              <div class="profile-field">
                <label>網站：</label>
                <a href="" target="">{{ formData.website || '(未填寫)' }}</a>
                <!-- 提示：有網站時綁定 href，沒有時禁用連結 -->
              </div>

              <div class="profile-meta">
                <!-- 提示：根據 isPublic 動態設定 data-* 屬性 -->
                <div>
                  <span>資料狀態：</span>
                  <span>{{ formData.isPublic ? '公開' : '私人' }}</span>
                </div>

                <div>
                  <span>電子報：</span>
                  <span>{{ formData.newsletter ? '已訂閱' : '未訂閱' }}</span>
                </div>
              </div>

              <button class="profile-button">
                儲存資料
                <!-- 提示：當必要欄位未填寫時禁用按鈕 -->
              </button>
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
          <span class="goal-icon">🔗</span>
          <span class="goal-text">掌握 v-bind 基礎語法和簡寫形式</span>
        </div>
        <div class="goal-item">
          <span class="goal-icon">🎨</span>
          <span class="goal-text">熟練使用動態 Class 和 Style 綁定</span>
        </div>
        <div class="goal-item">
          <span class="goal-icon">🔄</span>
          <span class="goal-text">理解屬性綁定中的條件邏輯</span>
        </div>
        <div class="goal-item">
          <span class="goal-icon">⚡</span>
          <span class="goal-text">學會處理響應式數據綁定</span>
        </div>
        <div class="goal-item">
          <span class="goal-icon">🛠️</span>
          <span class="goal-text">掌握實際應用場景的屬性綁定技巧</span>
        </div>
        <div class="goal-item">
          <span class="goal-icon">✨</span>
          <span class="goal-text">建立動態互動式用戶界面</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 任務一：基礎屬性綁定數據
const cardData = ref({
  imageUrl: '',
  title: '',
  linkUrl: ''
})

// const defaultImage = 'https://picsum.photos/300/200'

// 任務二：動態 Class 綁定數據
const cardState = ref({
  isActive: false,
  isHighlighted: false,
  hasError: false,
  size: 'medium'
})

// 任務三：Style 屬性綁定數據
const styleControls = ref({
  backgroundColor: '#3498db',
  textColor: '#ffffff',
  fontSize: 16,
  padding: 20,
  borderRadius: 8
})

// 任務四：條件屬性綁定數據
const formData = ref({
  username: '',
  email: '',
  website: '',
  isPublic: false,
  newsletter: false
})

// 輔助方法
const getCurrentClasses = () => {
  const classes = ['status-card']
  if (cardState.value.isActive) classes.push('active')
  if (cardState.value.isHighlighted) classes.push('highlighted')
  if (cardState.value.hasError) classes.push('error')
  classes.push(`size-${cardState.value.size}`)
  if (cardState.value.isActive && cardState.value.isHighlighted) {
    classes.push('featured')
  }
  return classes.join(' ')
}

// 計算屬性範例（供學員參考）
// const exampleComputedStyles = computed(() => ({
//   backgroundColor: styleControls.value.backgroundColor,
//   color: styleControls.value.textColor,
//   fontSize: styleControls.value.fontSize + 'px',
//   padding: styleControls.value.padding + 'px',
//   borderRadius: styleControls.value.borderRadius + 'px',
//   transition: 'all 0.3s ease'
// }))

const isValidEmail = computed(() => {
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  return emailRegex.test(formData.value.email)
})

// const isFormValid = computed(() => {
//   return formData.value.username.length >= 3 && isValidEmail.value
// })
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

.card-preview {
  background: white;
  border-radius: 8px;
  padding: 1rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.card-image {
  width: 100%;
  max-width: 300px;
  height: 200px;
  object-fit: cover;
  border-radius: 4px;
  margin-bottom: 1rem;
}

.card-link {
  display: inline-block;
  padding: 0.5rem 1rem;
  background: #3498db;
  color: white;
  text-decoration: none;
  border-radius: 4px;
  margin-top: 1rem;
}

.status-card {
  padding: 1.5rem;
  border-radius: 8px;
  background: white;
  border: 2px solid #e0e0e0;
  transition: all 0.3s ease;
  margin-bottom: 1rem;
}

.status-card.active {
  border-color: #27ae60;
  background: #e8f8f5;
}

.status-card.highlighted {
  box-shadow: 0 4px 15px rgba(52, 152, 219, 0.3);
}

.status-card.error {
  border-color: #e74c3c;
  background: #fdf2f2;
}

.status-card.featured {
  background: linear-gradient(45deg, #f39c12, #e67e22);
  color: white;
}

.status-card.size-small {
  padding: 1rem;
  font-size: 0.9rem;
}

.status-card.size-large {
  padding: 2rem;
  font-size: 1.1rem;
}

.class-info {
  padding: 0.5rem;
  background: #f8f9fa;
  border-radius: 4px;
  font-family: monospace;
  font-size: 0.9rem;
}

.styleable-box {
  padding: 2rem;
  text-align: center;
  border: 2px solid #ddd;
  border-radius: 8px;
  background: #f8f9fa;
}

.profile-card {
  background: white;
  border-radius: 8px;
  padding: 1.5rem;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.profile-field {
  display: flex;
  margin-bottom: 1rem;
  align-items: center;
}

.profile-field label {
  min-width: 80px;
  font-weight: 500;
  color: #666;
}

.profile-field span,
.profile-field a {
  margin-left: 1rem;
}

.profile-field.valid {
  color: #27ae60;
}

.profile-field.invalid {
  color: #e74c3c;
}

.profile-meta {
  margin: 1rem 0;
  padding: 1rem;
  background: #f8f9fa;
  border-radius: 4px;
}

.profile-button {
  width: 100%;
  padding: 0.8rem;
  background: #3498db;
  color: white;
  border: none;
  border-radius: 4px;
  font-size: 1rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

.profile-button:disabled {
  background: #bdc3c7;
  cursor: not-allowed;
}

.color-input {
  width: 60px;
  height: 40px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.range-input {
  margin: 0 1rem;
}
</style>
