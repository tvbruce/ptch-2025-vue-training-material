# 🧩 Vue3 組件化自我試煉

## 📋 項目概述

本項目為 Vue3 教學項目新增了「組件化自我試煉」功能，讓學員能夠通過實際操作來練習 Vue3 組件化開發的核心概念。

## 🎯 學習目標

通過完成這個任務管理系統，學員將掌握：

1. **Props 屬性傳遞** - 父組件向子組件傳遞數據
2. **Emit 事件處理** - 子組件向父組件發射事件
3. **插槽系統 (Slots)** - 使用具名插槽自定義組件內容
4. **組件間通信** - 實現複雜的父子組件交互
5. **可重用組件設計** - 創建靈活且可重用的 UI 組件
6. **組件生命週期** - 理解組件的創建和銷毀過程

## 📁 文件結構

```
src/components/ComponentSamples/
├── SelfChallengeDemo.vue          # 主要的試煉組件
└── components/                     # 子組件目錄
    ├── TaskItem.vue               # 任務項目組件
    ├── TaskForm.vue               # 任務表單組件
    ├── TaskFilter.vue             # 任務篩選組件
    ├── StatsCard.vue              # 統計卡片組件
    ├── EmptyState.vue             # 空狀態組件
    └── TaskDetail.vue             # 任務詳情組件
```

## 🔧 組件功能說明

### 1. SelfChallengeDemo.vue (主組件)

- **功能**: 任務管理系統的主要容器
- **特色**:
  - 統一的狀態管理
  - 組件間事件協調
  - 響應式數據處理
  - 完整的用戶界面

### 2. TaskItem.vue (任務項目)

- **Props**: `task` (任務對象)
- **Emits**: `toggle-complete`, `delete-task`, `edit-task`
- **插槽**: `actions` (自定義操作按鈕)
- **特色**:
  - 優先級視覺化
  - 完成狀態切換
  - 任務資訊展示

### 3. TaskForm.vue (任務表單)

- **Emits**: `add-task`
- **特色**:
  - 表單驗證
  - 即時預覽
  - 響應式設計
  - 錯誤處理

### 4. TaskFilter.vue (任務篩選)

- **Props**: `modelValue` (支援 v-model)
- **Emits**: `update:modelValue`, `filter-change`
- **特色**:
  - v-model 雙向綁定
  - 多條件篩選
  - 篩選狀態顯示

### 5. StatsCard.vue (統計卡片)

- **Props**: `title`, `value`, `color`, `trend`, `showProgress`
- **特色**:
  - 多種顏色主題
  - 趨勢指示器
  - 進度條顯示
  - 智能圖標選擇

### 6. EmptyState.vue (空狀態)

- **插槽**: `icon`, `title`, `description`, `actions`
- **Props**: `size`, `theme`, `animated`
- **特色**:
  - 完全可自定義
  - 多種尺寸和主題
  - 動畫效果

### 7. TaskDetail.vue (任務詳情)

- **Props**: `task`
- **Emits**: `close`, `update-task`
- **特色**:
  - 查看/編輯模式切換
  - 表單驗證
  - 模態框設計

## 🎮 使用方法

### 訪問試煉

1. 啟動開發服務器：`npm run dev`
2. 導航到「組件化」分類
3. 點擊「🎯 自我試煉」標籤

### 完成挑戰

學員需要根據 TODO 註解完成以下任務：

1. **Props 傳遞練習**

   - 在 `StatsCard` 組件中傳遞統計數據
   - 在 `TaskItem` 組件中傳遞任務對象

2. **事件發射練習**

   - 實現 `TaskForm` 的 `add-task` 事件
   - 實現 `TaskItem` 的各種操作事件

3. **插槽使用練習**

   - 在 `TaskItem` 中使用具名插槽
   - 在 `EmptyState` 中自定義內容

4. **v-model 實現**

   - 在 `TaskFilter` 中實現雙向綁定

5. **組件通信練習**
   - 實現完整的任務管理流程
   - 處理複雜的父子組件交互

## 💡 學習提示

### Props 最佳實踐

```javascript
// 定義 props 時要指定類型和驗證
const props = defineProps({
  task: {
    type: Object,
    required: true,
  },
  color: {
    type: String,
    default: 'blue',
    validator: (value) => ['blue', 'green', 'red'].includes(value),
  },
})
```

### Emit 事件處理

```javascript
// 定義要發射的事件
const emit = defineEmits(['add-task', 'delete-task'])

// 發射事件並傳遞數據
const handleSubmit = () => {
  emit('add-task', formData)
}
```

### 插槽使用

```vue
<!-- 在組件中定義插槽 -->
<template>
  <div class="card">
    <slot name="header">預設標題</slot>
    <slot>預設內容</slot>
    <slot name="footer"></slot>
  </div>
</template>

<!-- 在父組件中使用 -->
<MyCard>
  <template #header>自定義標題</template>
  <template #default>自定義內容</template>
  <template #footer>自定義底部</template>
</MyCard>
```

### v-model 實現

```javascript
// 子組件中支援 v-model
const props = defineProps(['modelValue'])
const emit = defineEmits(['update:modelValue'])

const updateValue = (newValue) => {
  emit('update:modelValue', newValue)
}
```

## 🎨 設計特色

- **現代化 UI**: 使用漸變色彩和陰影效果
- **響應式設計**: 支援各種螢幕尺寸
- **動畫效果**: 流暢的過渡和懸停效果
- **無障礙設計**: 良好的鍵盤導航和螢幕閱讀器支援
- **視覺回饋**: 清晰的狀態指示和操作回饋

## 🔍 技術亮點

1. **Composition API**: 全面使用 Vue3 的 Composition API
2. **TypeScript 友好**: 良好的類型定義和驗證
3. **模組化設計**: 每個組件職責單一且可重用
4. **性能優化**: 合理使用 computed 和 watch
5. **錯誤處理**: 完善的錯誤邊界和用戶提示

## 📚 延伸學習

完成基本挑戰後，學員可以嘗試：

1. **添加新功能**

   - 任務拖拽排序
   - 任務分組功能
   - 任務搜尋功能

2. **性能優化**

   - 使用 `v-memo` 優化列表渲染
   - 實現虛擬滾動
   - 添加 loading 狀態

3. **狀態管理**

   - 整合 Pinia 狀態管理
   - 實現數據持久化
   - 添加撤銷/重做功能

4. **測試覆蓋**
   - 編寫單元測試
   - 添加 E2E 測試
   - 組件快照測試

## 🎉 完成標準

學員完成以下項目即可視為通過挑戰：

- [ ] 所有 TODO 註解都已實現
- [ ] 任務的增刪改查功能正常
- [ ] 篩選和統計功能正確
- [ ] 組件間通信流暢
- [ ] 無 console 錯誤
- [ ] 響應式設計正常

## 🤝 技術支援

如果在完成挑戰過程中遇到問題，可以：

1. 查看瀏覽器開發者工具的 console
2. 檢查 Vue DevTools 中的組件狀態
3. 參考其他已完成的範例組件
4. 查閱 Vue3 官方文檔

---

**祝學習愉快！🚀**
