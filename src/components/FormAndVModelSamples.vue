<!-- components/FormAndVModelSamples.vue -->
<template>
  <div class="form-validation-demo">
    <h1>📝 表單輸入與 v-model</h1>
    <p class="route-info">📍 路徑：/FormAndVModelSamples.vue</p>
    <p class="description">
      掌握 Vue 3 的雙向數據綁定，學習如何在各種表單元素中使用 v-model，
      包含文本輸入、複選框、單選按鈕、下拉選擇框以及各種修飾符的使用。
    </p>

    <!-- 導航區域 -->
    <div class="demo-navigation">
      <button v-for="demo in demos" :key="demo.id" @click="currentDemo = demo.id" class="nav-btn"
        :class="{ active: currentDemo === demo.id }">
        {{ demo.icon }} {{ demo.title }}
      </button>
    </div>

    <!-- 當前示範組件 -->
    <component :is="currentComponent" />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 導入所有示範組件
import BasicInputDemo from './FormAndVModelSamples/BasicInputDemo.vue'
import CheckboxRadioDemo from './FormAndVModelSamples/CheckboxRadioDemo.vue'
import SelectDemo from './FormAndVModelSamples/SelectDemo.vue'
import ModifiersDemo from './FormAndVModelSamples/ModifiersDemo.vue'
import FormValidationDemo from './FormAndVModelSamples/FormValidationDemo.vue'
import UserRegistrationPractice from './FormAndVModelSamples/UserRegistrationPractice.vue'
import SelfChallengeDemo from './FormAndVModelSamples/SelfChallengeDemo.vue'
import SelfChallengeAnsweringArea from './FormAndVModelSamples/SelfChallengeAnsweringArea.vue'
import SelfChallengeSolution from './FormAndVModelSamples/SelfChallengeSolution.vue'
// 當前示範
const currentDemo = ref('basic')

// 所有示範配置
const demos = [
  {
    id: 'basic',
    title: '基礎輸入框',
    icon: '📝',
    component: BasicInputDemo,
    description: '文本、密碼、數字、日期時間等輸入框的 v-model 使用'
  },
  {
    id: 'checkbox',
    title: '複選框與單選按鈕',
    icon: '☑️',
    component: CheckboxRadioDemo,
    description: 'checkbox 和 radio button 的雙向綁定'
  },
  {
    id: 'select',
    title: '下拉選擇框',
    icon: '📋',
    component: SelectDemo,
    description: '單選和多選下拉框的數據綁定'
  },
  {
    id: 'modifiers',
    title: 'v-model 修飾符',
    icon: '⚙️',
    component: ModifiersDemo,
    description: '.lazy、.number、.trim 等修飾符的使用'
  },
  {
    id: 'validation',
    title: '表單驗證',
    icon: '✅',
    component: FormValidationDemo,
    description: '表單欄位驗證、即時驗證、自訂驗證規則'
  },
  {
    id: 'user-registration',
    title: '實際案例:用戶註冊',
    icon: '👤',
    component: UserRegistrationPractice,
    description: '用戶註冊表單、驗證規則、密碼強度檢查'
  },
  {
    id: 'self-challenge',
    title: '🎯 自我試煉題目',
    icon: '💪',
    component: SelfChallengeDemo,
    description: '自我試煉'
  },
  {
    id: 'self-challenge-answering-area',
    title: '🎯 自我試煉實作區域',
    icon: '💪',
    component: SelfChallengeAnsweringArea,
    description: '自我試煉實作區域'
  },
  {
    id: 'self-challenge-solution',
    title: '🎯 自我試煉解答',
    icon: '💪',
    component: SelfChallengeSolution,
    description: '自我試煉解答'
  }
]

// 組件映射
const componentMap = {
  basic: BasicInputDemo,
  checkbox: CheckboxRadioDemo,
  select: SelectDemo,
  modifiers: ModifiersDemo,
  validation: FormValidationDemo,
  'user-registration': UserRegistrationPractice,
  'self-challenge': SelfChallengeDemo,
  'self-challenge-answering-area': SelfChallengeAnsweringArea,
  'self-challenge-solution': SelfChallengeSolution
}

// 當前組件
const currentComponent = computed(() => {
  return componentMap[currentDemo.value]
})
</script>
