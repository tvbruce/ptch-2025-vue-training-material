<template>
    <div class="mouse-modifiers-demo">
        <h2>鼠標按鍵修飾符 (Mouse Button Modifiers)</h2>
        <p class="route-info">📍 路徑：/EventHandlingSamples/MouseModifiersDemo.vue</p>

        <!-- 基本鼠標按鍵修飾符 -->
        <div class="demo-section">
            <h3>1. 基本鼠標按鍵修飾符</h3>
            <div class="result">
                <div class="mouse-button-examples">
                    <div class="mouse-demo-area">
                        <div @click.left="handleLeftClick" @click.right="handleRightClick"
                            @click.middle="handleMiddleClick" @contextmenu.prevent class="click-area basic">
                            <h4>點擊測試區域</h4>
                            <p>左鍵點擊 | 右鍵點擊 | 中鍵點擊</p>
                            <p class="hint">右鍵點擊已阻止預設選單</p>
                        </div>
                    </div>

                    <div class="mouse-result">
                        <h5>鼠標點擊記錄:</h5>
                        <ul>
                            <li v-for="(action, index) in mouseActions" :key="index" :class="action.type">
                                <span class="timestamp">{{ action.timestamp }}</span>
                                <span class="action">{{ action.message }}</span>
                            </li>
                        </ul>
                        <button @click="clearMouseActions" class="btn btn-small btn-secondary">清除記錄</button>
                    </div>
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code><!-- 基本鼠標按鍵修飾符 -->
&lt;div @click.left="handleLeftClick"      <!-- 左鍵點擊 -->
     @click.right="handleRightClick"     <!-- 右鍵點擊 -->
     @click.middle="handleMiddleClick"   <!-- 中鍵點擊 -->
     @contextmenu.prevent&gt;               <!-- 阻止右鍵選單 -->
  點擊測試區域
&lt;/div&gt;</code></pre>
            </div>
        </div>

        <!-- 鼠標按鍵組合修飾符 -->
        <div class="demo-section">
            <h3>2. 鼠標按鍵與系統鍵組合</h3>
            <div class="result">
                <div class="combination-examples">
                    <div @click.left.ctrl="handleCtrlLeftClick" @click.left.shift="handleShiftLeftClick"
                        @click.left.alt="handleAltLeftClick" @click.right.ctrl="handleCtrlRightClick"
                        @contextmenu.prevent class="click-area combination">
                        <h4>組合鍵測試區域</h4>
                        <p>試試以下組合:</p>
                        <ul>
                            <li>Ctrl + 左鍵</li>
                            <li>Shift + 左鍵</li>
                            <li>Alt + 左鍵</li>
                            <li>Ctrl + 右鍵</li>
                        </ul>
                    </div>

                    <div class="combination-result">
                        <h5>組合鍵操作記錄:</h5>
                        <ul>
                            <li v-for="(action, index) in combinationActions" :key="index" :class="action.type">
                                <span class="timestamp">{{ action.timestamp }}</span>
                                <span class="action">{{ action.message }}</span>
                            </li>
                        </ul>
                        <button @click="clearCombinationActions" class="btn btn-small btn-secondary">清除記錄</button>
                    </div>
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code><!-- 鼠標按鍵與系統鍵組合 -->
&lt;div @click.left.ctrl="ctrlLeftHandler"    <!-- Ctrl + 左鍵 -->
     @click.left.shift="shiftLeftHandler"   <!-- Shift + 左鍵 -->
     @click.left.alt="altLeftHandler"       <!-- Alt + 左鍵 -->
     @click.right.ctrl="ctrlRightHandler"   <!-- Ctrl + 右鍵 -->
     @contextmenu.prevent&gt;
  組合鍵測試區域
&lt;/div&gt;</code></pre>
            </div>
        </div>

        <!-- 實際應用場景 -->
        <div class="demo-section">
            <h3>3. 實際應用場景</h3>
            <div class="result">
                <div class="practical-examples">
                    <!-- 檔案管理器模擬 -->
                    <div class="file-manager">
                        <h4>檔案管理器模擬</h4>
                        <div class="file-list">
                            <div v-for="file in files" :key="file.id" @click.left="selectFile(file)"
                                @click.left.ctrl.exact="toggleFileSelection(file)"
                                @click.left.shift.exact="rangeSelectFile(file)" @click.right="showContextMenu(file)"
                                @contextmenu.prevent :class="['file-item', { selected: file.selected }]">
                                <span class="file-icon">{{ file.icon }}</span>
                                <span class="file-name">{{ file.name }}</span>
                            </div>
                        </div>

                        <div class="selection-info">
                            <p><strong>已選擇:</strong> {{ selectedFiles.length }} 個檔案</p>
                            <p><strong>操作說明:</strong></p>
                            <ul>
                                <li>左鍵: 單選檔案</li>
                                <li>Ctrl + 左鍵: 多選/取消選擇</li>
                                <li>Shift + 左鍵: 範圍選擇</li>
                                <li>右鍵: 顯示選單</li>
                            </ul>
                        </div>
                    </div>

                    <!-- 繪圖工具模擬 -->
                    <div class="drawing-tool">
                        <h4>繪圖工具模擬</h4>
                        <div @mousedown.left="startDrawing" @mousedown.right="startErasing"
                            @mousedown.middle="startPanning" @mousemove="handleMouseMove" @mouseup="stopAction"
                            @contextmenu.prevent class="canvas-area" ref="canvasArea">
                            <p v-if="!isDrawing && !isErasing && !isPanning">
                                左鍵: 繪圖 | 右鍵: 擦除 | 中鍵: 平移
                            </p>
                            <p v-if="isDrawing" class="action-status drawing">🎨 繪圖模式</p>
                            <p v-if="isErasing" class="action-status erasing">🧽 擦除模式</p>
                            <p v-if="isPanning" class="action-status panning">✋ 平移模式</p>

                            <div v-for="dot in drawingDots" :key="dot.id" :style="{
                                left: dot.x + 'px',
                                top: dot.y + 'px',
                                backgroundColor: dot.color
                            }" class="drawing-dot"></div>
                        </div>

                        <div class="drawing-controls">
                            <button @click="clearCanvas" class="btn btn-small btn-secondary">清除畫布</button>
                            <span class="dot-count">點數: {{ drawingDots.length }}</span>
                        </div>
                    </div>
                </div>

                <div class="practical-result">
                    <h5>應用操作記錄:</h5>
                    <ul>
                        <li v-for="(action, index) in practicalActions" :key="index" :class="action.type">
                            <span class="timestamp">{{ action.timestamp }}</span>
                            <span class="action">{{ action.message }}</span>
                        </li>
                    </ul>
                    <button @click="clearPracticalActions" class="btn btn-small btn-secondary">清除記錄</button>
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code><!-- 檔案管理器範例 -->
&lt;div @click.left="selectFile"              <!-- 單選 -->
     @click.left.ctrl="toggleSelection"     <!-- 多選 -->
     @click.left.shift="rangeSelect"        <!-- 範圍選擇 -->
     @click.right="showContextMenu"         <!-- 右鍵選單 -->
     @contextmenu.prevent&gt;
  檔案項目
&lt;/div&gt;

<!-- 繪圖工具範例 -->
&lt;div @mousedown.left="startDrawing"        <!-- 開始繪圖 -->
     @mousedown.right="startErasing"        <!-- 開始擦除 -->
     @mousedown.middle="startPanning"       <!-- 開始平移 -->
     @mousemove="handleMouseMove"
     @mouseup="stopAction"
     @contextmenu.prevent&gt;
  畫布區域
&lt;/div&gt;</code></pre>
            </div>
        </div>

        <!-- 進階技巧 -->
        <div class="demo-section">
            <h3>4. 進階技巧與注意事項</h3>
            <div class="result">
                <div class="advanced-tips">
                    <div class="tip-card">
                        <h4>🎯 精確控制</h4>
                        <div @click.left.exact="handleExactLeft" @click.left.ctrl.exact="handleExactCtrlLeft"
                            @contextmenu.prevent class="exact-demo">
                            <p>使用 .exact 修飾符精確匹配</p>
                            <p>左鍵 (僅左鍵) | Ctrl+左鍵 (僅這個組合)</p>
                        </div>
                    </div>

                    <div class="tip-card">
                        <h4>🚫 阻止預設行為</h4>
                        <div @click.right.prevent="handlePreventRight" @click.middle.prevent="handlePreventMiddle"
                            class="prevent-demo">
                            <p>阻止瀏覽器預設行為</p>
                            <p>右鍵不會顯示選單 | 中鍵不會開啟新分頁</p>
                        </div>
                    </div>

                    <div class="tip-card">
                        <h4>⚡ 性能考量</h4>
                        <div class="performance-info">
                            <ul>
                                <li>使用 .passive 修飾符提升滾動性能</li>
                                <li>避免在高頻事件中執行複雜操作</li>
                                <li>適當使用 .once 修飾符</li>
                                <li>考慮使用防抖 (debounce) 技術</li>
                            </ul>
                        </div>
                    </div>
                </div>

                <div class="advanced-result">
                    <h5>進階操作記錄:</h5>
                    <ul>
                        <li v-for="(action, index) in advancedActions" :key="index" :class="action.type">
                            <span class="timestamp">{{ action.timestamp }}</span>
                            <span class="action">{{ action.message }}</span>
                        </li>
                    </ul>
                    <button @click="clearAdvancedActions" class="btn btn-small btn-secondary">清除記錄</button>
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code><!-- 精確控制範例 -->
&lt;div @click.left.exact="onlyLeftClick"           <!-- 僅左鍵 -->
     @click.left.ctrl.exact="onlyCtrlLeft"       <!-- 僅 Ctrl+左鍵 -->
     @click.right.prevent="preventRightClick"    <!-- 阻止右鍵預設 -->
     @click.middle.prevent="preventMiddleClick"  <!-- 阻止中鍵預設 -->
     @contextmenu.prevent&gt;
  精確控制區域
&lt;/div&gt;</code></pre>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 基本鼠標按鍵
const mouseActions = ref([])

const addMouseAction = (message, type = 'info') => {
    const timestamp = new Date().toLocaleTimeString()
    mouseActions.value.unshift({ timestamp, message, type })
    if (mouseActions.value.length > 10) {
        mouseActions.value.pop()
    }
}

const handleLeftClick = () => {
    addMouseAction('左鍵點擊', 'left')
}

const handleRightClick = () => {
    addMouseAction('右鍵點擊', 'right')
}

const handleMiddleClick = () => {
    addMouseAction('中鍵點擊', 'middle')
}

const clearMouseActions = () => {
    mouseActions.value = []
}

// 組合鍵
const combinationActions = ref([])

const addCombinationAction = (message, type = 'info') => {
    const timestamp = new Date().toLocaleTimeString()
    combinationActions.value.unshift({ timestamp, message, type })
    if (combinationActions.value.length > 10) {
        combinationActions.value.pop()
    }
}

const handleCtrlLeftClick = () => {
    addCombinationAction('Ctrl + 左鍵點擊', 'ctrl')
}

const handleShiftLeftClick = () => {
    addCombinationAction('Shift + 左鍵點擊', 'shift')
}

const handleAltLeftClick = () => {
    addCombinationAction('Alt + 左鍵點擊', 'alt')
}

const handleCtrlRightClick = () => {
    addCombinationAction('Ctrl + 右鍵點擊', 'ctrl')
}

const clearCombinationActions = () => {
    combinationActions.value = []
}

// 檔案管理器模擬
const files = ref([
    { id: 1, name: 'document.pdf', icon: '📄', selected: false },
    { id: 2, name: 'image.jpg', icon: '🖼️', selected: false },
    { id: 3, name: 'video.mp4', icon: '🎬', selected: false },
    { id: 4, name: 'music.mp3', icon: '🎵', selected: false },
    { id: 5, name: 'archive.zip', icon: '📦', selected: false },
    { id: 6, name: 'code.js', icon: '📝', selected: false }
])

const lastSelectedIndex = ref(-1)

const selectedFiles = computed(() => {
    return files.value.filter(file => file.selected)
})

const selectFile = (file) => {
    // 清除所有選擇
    files.value.forEach(f => f.selected = false)
    file.selected = true
    lastSelectedIndex.value = files.value.findIndex(f => f.id === file.id)
    addPracticalAction(`單選檔案: ${file.name}`, 'select')
}

const toggleFileSelection = (file) => {
    file.selected = !file.selected
    lastSelectedIndex.value = files.value.findIndex(f => f.id === file.id)
    addPracticalAction(`${file.selected ? '選擇' : '取消選擇'}檔案: ${file.name}`, 'toggle')
}

const rangeSelectFile = (file) => {
    const currentIndex = files.value.findIndex(f => f.id === file.id)
    if (lastSelectedIndex.value === -1) {
        selectFile(file)
        return
    }

    const start = Math.min(lastSelectedIndex.value, currentIndex)
    const end = Math.max(lastSelectedIndex.value, currentIndex)

    for (let i = start; i <= end; i++) {
        files.value[i].selected = true
    }

    addPracticalAction(`範圍選擇: ${end - start + 1} 個檔案`, 'range')
}

const showContextMenu = (file) => {
    addPracticalAction(`右鍵選單: ${file.name}`, 'context')
}

// 繪圖工具模擬
const isDrawing = ref(false)
const isErasing = ref(false)
const isPanning = ref(false)
const drawingDots = ref([])
const canvasArea = ref(null)

const startDrawing = (event) => {
    isDrawing.value = true
    addPracticalAction('開始繪圖', 'drawing')
    addDrawingDot(event, '#3498db')
}

const startErasing = (event) => {
    isErasing.value = true
    addPracticalAction('開始擦除', 'erasing')
    eraseNearbyDots(event)
}

const startPanning = () => {
    isPanning.value = true
    addPracticalAction('開始平移', 'panning')
}

const handleMouseMove = (event) => {
    if (isDrawing.value) {
        addDrawingDot(event, '#3498db')
    } else if (isErasing.value) {
        eraseNearbyDots(event)
    }
}

const stopAction = () => {
    if (isDrawing.value) {
        addPracticalAction('結束繪圖', 'drawing')
    } else if (isErasing.value) {
        addPracticalAction('結束擦除', 'erasing')
    } else if (isPanning.value) {
        addPracticalAction('結束平移', 'panning')
    }

    isDrawing.value = false
    isErasing.value = false
    isPanning.value = false
}

const addDrawingDot = (event, color) => {
    if (!canvasArea.value) return

    const rect = canvasArea.value.getBoundingClientRect()
    const x = event.clientX - rect.left
    const y = event.clientY - rect.top

    drawingDots.value.push({
        id: Date.now() + Math.random(),
        x: x - 3,
        y: y - 3,
        color
    })
}

const eraseNearbyDots = (event) => {
    if (!canvasArea.value) return

    const rect = canvasArea.value.getBoundingClientRect()
    const x = event.clientX - rect.left
    const y = event.clientY - rect.top

    drawingDots.value = drawingDots.value.filter(dot => {
        const distance = Math.sqrt((dot.x - x) ** 2 + (dot.y - y) ** 2)
        return distance > 20
    })
}

const clearCanvas = () => {
    drawingDots.value = []
    addPracticalAction('清除畫布', 'clear')
}

// 實際應用記錄
const practicalActions = ref([])

const addPracticalAction = (message, type = 'info') => {
    const timestamp = new Date().toLocaleTimeString()
    practicalActions.value.unshift({ timestamp, message, type })
    if (practicalActions.value.length > 15) {
        practicalActions.value.pop()
    }
}

const clearPracticalActions = () => {
    practicalActions.value = []
}

// 進階技巧
const advancedActions = ref([])

const addAdvancedAction = (message, type = 'info') => {
    const timestamp = new Date().toLocaleTimeString()
    advancedActions.value.unshift({ timestamp, message, type })
    if (advancedActions.value.length > 10) {
        advancedActions.value.pop()
    }
}

const handleExactLeft = () => {
    addAdvancedAction('精確左鍵點擊 (僅左鍵)', 'exact')
}

const handleExactCtrlLeft = () => {
    addAdvancedAction('精確 Ctrl+左鍵 (僅此組合)', 'exact')
}

const handlePreventRight = () => {
    addAdvancedAction('右鍵點擊 (已阻止預設行為)', 'prevent')
}

const handlePreventMiddle = () => {
    addAdvancedAction('中鍵點擊 (已阻止預設行為)', 'prevent')
}

const clearAdvancedActions = () => {
    advancedActions.value = []
}
</script>
