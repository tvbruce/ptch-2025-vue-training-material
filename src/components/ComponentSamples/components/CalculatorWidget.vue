<template>
  <div class="calculator-widget">
    <h5>計算器小工具</h5>
    <div class="widget-content">
      <div class="calculator-display">
        {{ displayExpression }}
      </div>
      <div class="calculator-keypad">
        <div class="calc-row">
          <button @click="clear" class="btn btn-secondary calc-btn">C</button>
          <button @click="deleteLast" class="btn btn-secondary calc-btn">⌫</button>
          <button @click="inputOperator('/')" class="btn btn-warning calc-btn">÷</button>
          <button @click="inputOperator('*')" class="btn btn-warning calc-btn">×</button>
        </div>
        <div class="calc-row">
          <button @click="inputNumber('7')" class="btn btn-primary calc-btn">7</button>
          <button @click="inputNumber('8')" class="btn btn-primary calc-btn">8</button>
          <button @click="inputNumber('9')" class="btn btn-primary calc-btn">9</button>
          <button @click="inputOperator('-')" class="btn btn-warning calc-btn">-</button>
        </div>
        <div class="calc-row">
          <button @click="inputNumber('4')" class="btn btn-primary calc-btn">4</button>
          <button @click="inputNumber('5')" class="btn btn-primary calc-btn">5</button>
          <button @click="inputNumber('6')" class="btn btn-primary calc-btn">6</button>
          <button @click="inputOperator('+')" class="btn btn-warning calc-btn">+</button>
        </div>
        <div class="calc-row">
          <button @click="inputNumber('1')" class="btn btn-primary calc-btn">1</button>
          <button @click="inputNumber('2')" class="btn btn-primary calc-btn">2</button>
          <button @click="inputNumber('3')" class="btn btn-primary calc-btn">3</button>
          <button @click="calculate" class="btn btn-success calc-btn calc-equals">=</button>
        </div>
        <div class="calc-row">
          <button @click="inputNumber('0')" class="btn btn-primary calc-btn calc-zero">0</button>
          <button @click="inputNumber('.')" class="btn btn-primary calc-btn">.</button>
        </div>
      </div>
      <div class="widget-info">
        <p>計算次數: {{ calculationCount }}</p>
        <p>最後結果: {{ lastResult || '無' }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const emit = defineEmits(['widget-action', 'value-changed'])

const display = ref('0')
const operator = ref('')
const previousInput = ref('')
const calculationCount = ref(0)
const lastResult = ref('')
const shouldReplaceDisplay = ref(false)

// 計算顯示的運算式
const displayExpression = computed(() => {
  if (operator.value && previousInput.value) {
    const operatorMap = {
      '+': ' + ',
      '-': ' - ',
      '*': ' × ',
      '/': ' ÷ '
    }
    return `${previousInput.value}${operatorMap[operator.value]}${display.value}`
  }
  return display.value
})

const inputNumber = (num) => {
  if (display.value === '0' || shouldReplaceDisplay.value) {
    display.value = num
    shouldReplaceDisplay.value = false
  } else {
    display.value += num
  }
  emit('widget-action', `輸入數字: ${num}`)
}

const inputOperator = (op) => {
  if (operator.value && !shouldReplaceDisplay.value) {
    calculate()
  }

  previousInput.value = display.value
  operator.value = op
  shouldReplaceDisplay.value = true

  const operatorMap = {
    '+': '加',
    '-': '減',
    '*': '乘',
    '/': '除'
  }
  emit('widget-action', `輸入運算符: ${operatorMap[op]}`)
}

const calculate = () => {
  if (!previousInput.value || !operator.value) return

  const prev = parseFloat(previousInput.value)
  const current = parseFloat(display.value)
  let result

  switch (operator.value) {
    case '+':
      result = prev + current
      break
    case '-':
      result = prev - current
      break
    case '*':
      result = prev * current
      break
    case '/':
      result = current !== 0 ? prev / current : 'Error'
      break
    default:
      return
  }

  if (result === 'Error') {
    display.value = 'Error'
    lastResult.value = 'Error'
  } else {
    if (Number.isInteger(result)) {
      display.value = result.toString()
    } else {
      display.value = parseFloat(result.toFixed(10)).toString()
    }
    lastResult.value = display.value
  }

  calculationCount.value++
  previousInput.value = ''
  operator.value = ''
  shouldReplaceDisplay.value = true

  emit('widget-action', '執行計算')
  emit('value-changed', result === 'Error' ? 0 : result)
}

const clear = () => {
  display.value = '0'
  operator.value = ''
  previousInput.value = ''
  shouldReplaceDisplay.value = false
  emit('widget-action', '清除')
}

const deleteLast = () => {
  if (display.value.length > 1) {
    display.value = display.value.slice(0, -1)
  } else {
    display.value = '0'
  }
  emit('widget-action', '刪除最後一位')
}
</script>
