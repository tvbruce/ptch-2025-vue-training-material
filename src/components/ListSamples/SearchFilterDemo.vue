<template>
  <div class="list-rendering-demo">
    <h2>搜尋與過濾</h2>
    <p class="route-info">📍 路徑：/ListSamples/SearchFilterDemo.vue</p>
    <p class="description">
      在搜索、篩選等場景中替換數組時，正確的 key 能保持元素的一致性
    </p>

    <div class="demo-section">
      <h3>✅ 產品搜索篩選 (使用唯一 ID 作為 key) <span class="code-path">SearchFilterDemo.vue</span></h3>
      <div class="controls">
        <input v-model="searchTerm" placeholder="搜索產品名稱..." class="search-input" @input="searchProducts">
        <button @click="resetProducts" class="btn btn-secondary">重置</button>
      </div>
      <div class="result">
        <div class="search-info">
          找到 {{ filteredProducts.length }} 個產品
        </div>
        <div class="product-list">
          <div v-for="product in filteredProducts" :key="product.id" class="product-item good-example">
            <div class="product-info">
              <span class="product-name">{{ product.name }}</span>
              <span class="product-price">${{ product.price }}</span>
              <span class="product-id">ID: {{ product.id }}</span>
            </div>
            <div class="product-description">
              {{ product.description }}
            </div>
            <div class="product-meta">
              <span class="product-category">分類：{{ product.category }}</span>
              <span class="product-stock">庫存：{{ product.stock }}</span>
              <span class="product-rating">評分：{{ product.rating }}/5</span>
            </div>
          </div>
        </div>
      </div>
      <div class="code-example">
        <pre v-pre><code>// 搜索功能實現
const searchProducts = () => {
  const term = searchTerm.value.toLowerCase().trim()
  if (term === '') {
    filteredProducts.value = [...originalProducts]
  } else {
    filteredProducts.value = originalProducts.filter(product =>
      product.name.toLowerCase().includes(term)
    )
  }
}

// 模板中使用唯一 key
&lt;div v-for="product in filteredProducts" :key="product.id"&gt;</code></pre>
      </div>
    </div>

    <div class="demo-section">
      <h3>🔍 測試步驟 <span class="code-path">測試指南</span></h3>
      <div class="result">
        <div class="explanation">
          <ol>
            <li>觀察初始狀態下的產品列表展示</li>
            <li>在搜索框中輸入關鍵字（例如：「手機」、「筆」等）</li>
            <li>觀察篩選後的結果，注意產品的展示順序和內容</li>
            <li>清空搜索框，觀察恢復完整列表時的狀態</li>
            <li>重複搜索不同關鍵字，觀察列表更新的流暢度</li>
          </ol>
        </div>
      </div>
    </div>

    <div class="demo-section">
      <h3>💡 關鍵優勢 <span class="code-path">最佳實踐</span></h3>
      <div class="result">
        <div class="key-point">
          <p>使用 <code>:key="product.id"</code> 確保每個產品都能被正確追蹤，當搜索結果改變時，Vue 能高效地更新 DOM，避免不必要的元素重建，提升性能和用戶體驗。</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// 產品數據
const originalProducts = [
  {
    id: 101,
    name: 'iPhone 15 Pro',
    price: 999,
    description: '最新的 iPhone 旗艦機型，搭載 A17 Pro 處理器',
    category: '手機',
    stock: 50,
    rating: 4.8
  },
  {
    id: 102,
    name: 'Samsung Galaxy S24',
    price: 899,
    description: '三星最新旗艦手機，配備先進的 AI 攝影功能',
    category: '手機',
    stock: 35,
    rating: 4.6
  },
  {
    id: 103,
    name: 'MacBook Pro',
    price: 1999,
    description: '專業級筆記型電腦，搭載 M3 晶片',
    category: '電腦',
    stock: 20,
    rating: 4.9
  },
  {
    id: 104,
    name: 'iPad Air',
    price: 599,
    description: '輕薄平板電腦，適合創作和娛樂',
    category: '平板',
    stock: 40,
    rating: 4.5
  },
  {
    id: 105,
    name: 'AirPods Pro',
    price: 249,
    description: '主動降噪無線耳機，音質卓越',
    category: '耳機',
    stock: 100,
    rating: 4.7
  },
  {
    id: 106,
    name: 'Apple Watch',
    price: 399,
    description: '智慧手錶，健康監測功能完善',
    category: '穿戴',
    stock: 60,
    rating: 4.4
  },
  {
    id: 107,
    name: '筆記型電腦',
    price: 1299,
    description: '高性能商務筆電，續航力強',
    category: '電腦',
    stock: 25,
    rating: 4.3
  },
  {
    id: 108,
    name: '無線滑鼠',
    price: 79,
    description: '人體工學設計，精準操控',
    category: '配件',
    stock: 200,
    rating: 4.2
  },
  {
    id: 109,
    name: '機械鍵盤',
    price: 159,
    description: '青軸機械鍵盤，打字手感極佳',
    category: '配件',
    stock: 80,
    rating: 4.6
  },
  {
    id: 110,
    name: '顯示器',
    price: 299,
    description: '27吋 4K 顯示器，色彩鮮豔',
    category: '顯示器',
    stock: 30,
    rating: 4.5
  },
  {
    id: 111,
    name: '手機殼',
    price: 29,
    description: '透明防摔手機保護殼',
    category: '配件',
    stock: 500,
    rating: 4.1
  },
  {
    id: 112,
    name: '充電器',
    price: 49,
    description: '快充充電器，支援多種設備',
    category: '配件',
    stock: 150,
    rating: 4.3
  }
]

// 搜索相關
const searchTerm = ref('')

// 篩選後的產品列表
const filteredProducts = ref([...originalProducts])

// 搜索功能
const searchProducts = () => {
  const term = searchTerm.value.toLowerCase().trim()
  if (term === '') {
    filteredProducts.value = [...originalProducts]
  } else {
    filteredProducts.value = originalProducts.filter(product =>
      product.name.toLowerCase().includes(term)
    )
  }
}

const resetProducts = () => {
  searchTerm.value = ''
  filteredProducts.value = [...originalProducts]
}
</script>
