<template>
    <div class="key-modifiers-demo">
        <h2>按鍵修飾符 (Key Modifiers)</h2>
        <p class="route-info">📍 路徑：/EventHandlingSamples/KeyModifiersDemo.vue</p>

        <!-- 常用按鍵修飾符 -->
        <div class="demo-section">
            <h3>1. 常用按鍵修飾符</h3>
            <div class="result">
                <div class="key-examples">
                    <div class="input-group">
                        <label>按 Enter 提交:</label>
                        <input @keyup.enter="handleEnter" v-model="enterInput" placeholder="輸入後按 Enter"
                            class="input-field">
                    </div>

                    <div class="input-group">
                        <label>按 Tab 切換:</label>
                        <input @keydown.tab="handleTab" v-model="tabInput" placeholder="按 Tab 試試" class="input-field">
                    </div>

                    <div class="input-group">
                        <label>按 Delete 清除:</label>
                        <input @keyup.delete="handleDelete" v-model="deleteInput" placeholder="按 Delete 清除"
                            class="input-field">
                    </div>

                    <div class="input-group">
                        <label>按 Esc 取消:</label>
                        <input @keyup.esc="handleEscape" v-model="escInput" placeholder="按 Esc 取消" class="input-field">
                    </div>

                    <div class="input-group">
                        <label>按 Space 確認:</label>
                        <input @keyup.space="handleSpace" v-model="spaceInput" placeholder="按空格鍵確認" class="input-field">
                    </div>
                </div>

                <div class="key-result">
                    <h5>按鍵操作結果:</h5>
                    <ul>
                        <li v-for="(action, index) in keyActions" :key="index">
                            {{ action }}
                        </li>
                    </ul>
                    <button @click="clearKeyActions" class="btn btn-small btn-secondary">清除記錄</button>
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code><!-- 常用按鍵修飾符 -->
&lt;input @keyup.enter="handleEnter"&gt;     <!-- Enter 鍵 -->
&lt;input @keydown.tab="handleTab"&gt;       <!-- Tab 鍵 -->
&lt;input @keyup.delete="handleDelete"&gt;   <!-- Delete 鍵 -->
&lt;input @keyup.esc="handleEscape"&gt;      <!-- Escape 鍵 -->
&lt;input @keyup.space="handleSpace"&gt;     <!-- 空格鍵 --></code></pre>
            </div>
        </div>

        <!-- 方向鍵修飾符 -->
        <div class="demo-section">
            <h3>2. 方向鍵修飾符</h3>
            <div class="result">
                <div class="arrow-demo">
                    <div class="game-area" @keyup.up="moveUp" @keyup.down="moveDown" @keyup.left="moveLeft"
                        @keyup.right="moveRight" tabindex="0">
                        <p>點擊這裡後使用方向鍵移動</p>
                        <div class="player" :style="{ top: playerPosition.y + 'px', left: playerPosition.x + 'px' }">
                            🎮
                        </div>
                    </div>
                    <div class="controls-info">
                        <p><strong>位置:</strong> X: {{ playerPosition.x }}, Y: {{ playerPosition.y }}</p>
                        <p><strong>移動記錄:</strong> {{ moveHistory.join(' → ') }}</p>
                        <button @click="resetPosition" class="btn btn-small btn-primary">重置位置</button>
                    </div>
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code><!-- 方向鍵修飾符 -->
&lt;div @keyup.up="moveUp"         <!-- ↑ 鍵 -->
     @keyup.down="moveDown"       <!-- ↓ 鍵 -->
     @keyup.left="moveLeft"       <!-- ← 鍵 -->
     @keyup.right="moveRight"     <!-- → 鍵 -->
     tabindex="0"&gt;
  可聚焦元素
&lt;/div&gt;</code></pre>
            </div>
        </div>

        <!-- 系統修飾符 -->
        <div class="demo-section">
            <h3>3. 系統修飾符</h3>
            <div class="result">
                <div class="system-modifiers">
                    <div class="input-group">
                        <label>Ctrl + Enter 快速提交:</label>
                        <textarea @keyup.ctrl.enter="handleCtrlEnter" v-model="ctrlText"
                            placeholder="輸入文字，然後 Ctrl + Enter" class="textarea-field"></textarea>
                    </div>

                    <div class="input-group">
                        <label>Alt + S 快速儲存:</label>
                        <input @keyup.alt.s="handleAltSave" v-model="altText" placeholder="Alt + S 儲存"
                            class="input-field">
                    </div>

                    <div class="input-group">
                        <label>Shift + Delete 強制刪除:</label>
                        <input @keyup.shift.delete="handleShiftDelete" v-model="shiftText"
                            placeholder="Shift + Delete 強制刪除" class="input-field">
                    </div>

                    <div class="input-group">
                        <label>Meta + Z 撤銷 (Mac: Cmd, Win: Win鍵):</label>
                        <input @keyup.meta.z="handleMetaUndo" v-model="metaText" placeholder="Meta + Z 撤銷"
                            class="input-field">
                    </div>
                </div>

                <div class="system-result">
                    <h5>系統組合鍵結果:</h5>
                    <ul>
                        <li v-for="(action, index) in systemActions" :key="index">
                            {{ action }}
                        </li>
                    </ul>
                    <button @click="clearSystemActions" class="btn btn-small btn-secondary">清除記錄</button>
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code><!-- 系統修飾符組合 -->
&lt;input @keyup.ctrl.enter="ctrlEnterHandler"&gt;
&lt;input @keyup.alt.s="altSaveHandler"&gt;
&lt;input @keyup.shift.delete="shiftDeleteHandler"&gt;
&lt;input @keyup.meta.z="metaUndoHandler"&gt;

<!-- 可以組合多個系統修飾符 -->
&lt;input @keyup.ctrl.shift.s="advancedSave"&gt;</code></pre>
            </div>
        </div>

        <!-- 實用快捷鍵範例 -->
        <div class="demo-section">
            <h3>4. 實用快捷鍵組合範例</h3>
            <div class="result">
                <div class="shortcut-demo">
                    <div class="editor-area" tabindex="0" @keyup.ctrl.s="saveDocument" @keyup.ctrl.z="undoAction"
                        @keyup.ctrl.y="redoAction" @keyup.ctrl.a="selectAll" @keyup.f5="refreshView">
                        <h4>模擬編輯器 (點擊這裡獲得焦點)</h4>
                        <textarea v-model="editorContent" placeholder="在這裡輸入內容..." class="editor-content"></textarea>
                        <div class="shortcut-hints">
                            <p><strong>可用快捷鍵:</strong></p>
                            <ul>
                                <li>Ctrl + S: 儲存</li>
                                <li>Ctrl + Z: 撤銷</li>
                                <li>Ctrl + Y: 重做</li>
                                <li>Ctrl + A: 全選</li>
                                <li>F5: 重新整理</li>
                            </ul>
                        </div>
                    </div>

                    <div class="shortcut-result">
                        <h5>快捷鍵操作記錄:</h5>
                        <ul>
                            <li v-for="(action, index) in shortcutActions" :key="index">
                                {{ action }}
                            </li>
                        </ul>
                        <button @click="clearShortcutActions" class="btn btn-small btn-secondary">清除記錄</button>
                    </div>
                </div>
            </div>
            <div class="code-example">
                <pre v-pre><code><!-- 實用快捷鍵組合 -->
&lt;div @keyup.ctrl.s="saveDocument"      <!-- Ctrl + S 儲存 -->
     @keyup.ctrl.z="undoAction"         <!-- Ctrl + Z 撤銷 -->
     @keyup.ctrl.y="redoAction"         <!-- Ctrl + Y 重做 -->
     @keyup.ctrl.a="selectAll"          <!-- Ctrl + A 全選 -->
     @keyup.f5="refreshView"            <!-- F5 重新整理 -->
     tabindex="0"&gt;
  編輯器內容
&lt;/div&gt;</code></pre>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'

// 常用按鍵修飾符
const enterInput = ref('')
const tabInput = ref('')
const deleteInput = ref('')
const escInput = ref('')
const spaceInput = ref('')
const keyActions = ref([])

const addKeyAction = (action) => {
    const timestamp = new Date().toLocaleTimeString()
    keyActions.value.unshift(`${timestamp} - ${action}`)
    if (keyActions.value.length > 10) keyActions.value.pop()
}

const handleEnter = () => {
    addKeyAction(`Enter 鍵觸發，內容: "${enterInput.value}"`)
}

const handleTab = () => {
    addKeyAction(`Tab 鍵觸發，內容: "${tabInput.value}"`)
}

const handleDelete = () => {
    deleteInput.value = ''
    addKeyAction('Delete 鍵觸發，內容已清除')
}

const handleEscape = () => {
    escInput.value = ''
    addKeyAction('Escape 鍵觸發，內容已取消')
}

const handleSpace = () => {
    addKeyAction(`Space 鍵觸發，內容確認: "${spaceInput.value}"`)
}

const clearKeyActions = () => {
    keyActions.value = []
}

// 方向鍵範例
const playerPosition = ref({ x: 100, y: 100 })
const moveHistory = ref([])

const moveUp = () => {
    playerPosition.value.y = Math.max(0, playerPosition.value.y - 20)
    moveHistory.value.push('上')
    if (moveHistory.value.length > 10) moveHistory.value.shift()
}

const moveDown = () => {
    playerPosition.value.y = Math.min(200, playerPosition.value.y + 20)
    moveHistory.value.push('下')
    if (moveHistory.value.length > 10) moveHistory.value.shift()
}

const moveLeft = () => {
    playerPosition.value.x = Math.max(0, playerPosition.value.x - 20)
    moveHistory.value.push('左')
    if (moveHistory.value.length > 10) moveHistory.value.shift()
}

const moveRight = () => {
    playerPosition.value.x = Math.min(300, playerPosition.value.x + 20)
    moveHistory.value.push('右')
    if (moveHistory.value.length > 10) moveHistory.value.shift()
}

const resetPosition = () => {
    playerPosition.value = { x: 100, y: 100 }
    moveHistory.value = []
}

// 系統修飾符
const ctrlText = ref('')
const altText = ref('')
const shiftText = ref('')
const metaText = ref('')
const systemActions = ref([])

const addSystemAction = (action) => {
    const timestamp = new Date().toLocaleTimeString()
    systemActions.value.unshift(`${timestamp} - ${action}`)
    if (systemActions.value.length > 8) systemActions.value.pop()
}

const handleCtrlEnter = () => {
    addSystemAction(`Ctrl + Enter: 快速提交 "${ctrlText.value}"`)
}

const handleAltSave = () => {
    addSystemAction(`Alt + S: 快速儲存 "${altText.value}"`)
}

const handleShiftDelete = () => {
    const content = shiftText.value
    shiftText.value = ''
    addSystemAction(`Shift + Delete: 強制刪除 "${content}"`)
}

const handleMetaUndo = () => {
    addSystemAction(`Meta + Z: 撤銷操作 "${metaText.value}"`)
}

const clearSystemActions = () => {
    systemActions.value = []
}

// 快捷鍵範例
const editorContent = ref('在這裡輸入一些內容來測試快捷鍵...')
const shortcutActions = ref([])

const addShortcutAction = (action) => {
    const timestamp = new Date().toLocaleTimeString()
    shortcutActions.value.unshift(`${timestamp} - ${action}`)
    if (shortcutActions.value.length > 10) shortcutActions.value.pop()
}

const saveDocument = () => {
    addShortcutAction('📄 文件已儲存 (Ctrl + S)')
}

const undoAction = () => {
    addShortcutAction('↶ 撤銷操作 (Ctrl + Z)')
}

const redoAction = () => {
    addShortcutAction('↷ 重做操作 (Ctrl + Y)')
}

const selectAll = () => {
    addShortcutAction('📝 全選文字 (Ctrl + A)')
}

const refreshView = () => {
    addShortcutAction('🔄 重新整理檢視 (F5)')
}

const clearShortcutActions = () => {
    shortcutActions.value = []
}
</script>
