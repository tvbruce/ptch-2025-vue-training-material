<template>
  <div class="list-rendering-demo">
    <h2>分類切換列表</h2>
    <p class="route-info">📍 路徑：/ListSamples/CategorySwitchDemo.vue</p>
    <p class="description">
      在電商網站、內容管理等場景中，經常需要切換不同分類來顯示不同的商品列表
    </p>

    <div class="demo-section">
      <h3>✅ 商品分類切換 (正確使用 key) <span class="code-path">CategorySwitchDemo.vue</span></h3>
      <div class="controls">
        <button v-for="category in categories" :key="category.id" @click="switchCategory(category.id)"
          :class="['btn', currentCategory === category.id ? 'btn-primary' : 'btn-secondary']">
          {{ category.name }}
        </button>
      </div>

      <div class="result">
        <div class="category-info">
          當前分類：{{ getCurrentCategoryName(currentCategory) }}
          (共 {{ currentBooks.length }} 本書)
        </div>

        <div class="book-list">
          <div v-for="book in currentBooks" :key="book.id" class="book-item good-example">
            <div class="book-info">
              <span class="book-title">{{ book.title }}</span>
              <span class="book-author">作者：{{ book.author }}</span>
              <span class="book-price">${{ book.price }}</span>
              <span class="book-id">ID: {{ book.id }}</span>
            </div>
            <div class="book-description">
              {{ book.description }}
            </div>
            <div class="book-meta">
              <span class="book-category">分類：{{ getCurrentCategoryName(currentCategory) }}</span>
              <span class="book-pages">頁數：{{ book.pages }}</span>
              <span class="book-rating">評分：{{ book.rating }}/5</span>
            </div>
          </div>
        </div>
      </div>

      <div class="code-example">
        <pre v-pre><code>// 分類切換實現
const currentCategory = ref('novel')
const currentBooks = computed(() => booksByCategory[currentCategory.value])

const switchCategory = (categoryId) => {
  currentCategory.value = categoryId
}

// 模板中使用唯一 key
&lt;div v-for="book in currentBooks" :key="book.id"&gt;</code></pre>
      </div>

      <div class="explanation">
        <h4>🔍 觀察重點：</h4>
        <ol>
          <li>切換不同分類時，列表內容完全替換</li>
          <li>每本書都有唯一的 ID，確保 Vue 能正確追蹤</li>
          <li>即使不同分類間可能有相同的索引位置，但因為使用了唯一 key，不會產生錯誤的 DOM 復用</li>
          <li>觀察切換時的動畫效果，可以看出 Vue 正確地創建和銷毀了不同的元素</li>
        </ol>

        <div class="key-point">
          <h4>💡 關鍵點：</h4>
          <p>使用 <code>:key="book.id"</code> 確保每本書都有唯一標識，即使在不同分類間切換，Vue 也能正確追蹤每個書籍元素的狀態。</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 書籍分類數據
const categories = [
  { id: 'novel', name: '小說' },
  { id: 'tech', name: '科技' },
  { id: 'history', name: '歷史' }
]

const booksByCategory = {
  novel: [
    {
      id: 201,
      title: '追風箏的人',
      author: '卡勒德·胡賽尼',
      price: 280,
      description: '一個關於友誼、背叛與救贖的動人故事，背景設在阿富汗的政治動盪時期。',
      pages: 416,
      rating: 4.8
    },
    {
      id: 202,
      title: '百年孤寂',
      author: '馬奎斯',
      price: 320,
      description: '魔幻寫實主義的經典之作，講述布恩迪亞家族七代人的興衰史。',
      pages: 448,
      rating: 4.6
    },
    {
      id: 203,
      title: '挪威的森林',
      author: '村上春樹',
      price: 300,
      description: '青春、愛情與成長的故事，充滿了淡淡的憂鬱與哲思。',
      pages: 384,
      rating: 4.5
    },
    {
      id: 204,
      title: '1984',
      author: '喬治·歐威爾',
      price: 250,
      description: '反烏托邦小說的代表作，描繪極權主義社會的恐怖景象。',
      pages: 368,
      rating: 4.7
    }
  ],
  tech: [
    {
      id: 301,
      title: 'JavaScript 權威指南',
      author: 'David Flanagan',
      price: 680,
      description: 'JavaScript 開發者的聖經，涵蓋語言核心特性與 Web API。',
      pages: 1096,
      rating: 4.4
    },
    {
      id: 302,
      title: 'Vue.js 實戰',
      author: '梁灝',
      price: 520,
      description: '深入淺出介紹 Vue.js 框架，從基礎到進階應用。',
      pages: 512,
      rating: 4.3
    },
    {
      id: 303,
      title: '演算法導論',
      author: 'Thomas H. Cormen',
      price: 890,
      description: '計算機科學領域的經典教材，全面介紹演算法設計與分析。',
      pages: 1312,
      rating: 4.6
    },
    {
      id: 304,
      title: '設計模式',
      author: 'Gang of Four',
      price: 650,
      description: '軟體設計模式的經典著作，程式設計師必讀書籍。',
      pages: 395,
      rating: 4.5
    }
  ],
  history: [
    {
      id: 401,
      title: '人類簡史',
      author: '哈拉瑞',
      price: 450,
      description: '從認知革命到科學革命，重新審視人類發展的歷程。',
      pages: 448,
      rating: 4.7
    },
    {
      id: 402,
      title: '槍炮、病菌與鋼鐵',
      author: '賈德·戴蒙',
      price: 420,
      description: '探討人類社會不平等的起源，獲得普立茲獎的傑作。',
      pages: 512,
      rating: 4.6
    },
    {
      id: 403,
      title: '史記',
      author: '司馬遷',
      price: 380,
      description: '中國第一部紀傳體通史，被譽為「史家之絕唱」。',
      pages: 3200,
      rating: 4.9
    },
    {
      id: 404,
      title: '資治通鑑',
      author: '司馬光',
      price: 580,
      description: '中國古代編年體史書的代表作，記載1362年的歷史。',
      pages: 2940,
      rating: 4.8
    }
  ]
}

// 分類切換狀態
const currentCategory = ref('novel')

// 當前顯示的書籍列表
const currentBooks = computed(() => booksByCategory[currentCategory.value])

// 分類切換方法
const switchCategory = (categoryId) => {
  currentCategory.value = categoryId
}

const getCurrentCategoryName = (categoryId) => {
  return categories.find(cat => cat.id === categoryId)?.name || ''
}
</script>
