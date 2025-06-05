<template>
    <div class="solution">
        <h2>✅ 解答 - v-for 列表渲染</h2>
        <p>完整實現學生成績管理系統，展示各種 v-for 渲染技巧</p>

        <!-- 新增學生表單 -->
        <div class="demo-card">
            <h4>新增學生</h4>
            <form @submit.prevent="addStudent" class="add-form">
                <input v-model="newStudent.name" placeholder="學生姓名" required />
                <input v-model="newStudent.subject" placeholder="科目" required />
                <input v-model.number="newStudent.score" type="number" min="0" max="100" placeholder="分數" required />
                <button type="submit">新增學生</button>
            </form>
        </div>

        <!-- 學生列表 -->
        <div class="demo-card">
            <h4>學生列表 ({{ students.length }} 位學生)</h4>
            <div v-if="students.length === 0" class="empty-state">
                <p>目前沒有學生資料，請新增學生</p>
            </div>

            <div v-else class="student-list">
                <div v-for="student in students" :key="student.id" class="student-card"
                    :class="{ editing: editingId === student.id }">
                    <!-- 正常顯示模式 -->
                    <template v-if="editingId !== student.id">
                        <div class="student-info">
                            <h5>{{ student.name }}</h5>
                            <p><strong>科目：</strong>{{ student.subject }}</p>
                            <p><strong>分數：</strong>{{ student.score }} 分</p>
                            <div class="grade-badge" :class="getGradeClass(student.score)">
                                {{ getGrade(student.score) }}
                            </div>
                        </div>
                        <div class="student-actions">
                            <button @click="editStudent(student)" class="edit-btn">編輯</button>
                            <button @click="deleteStudent(student.id)" class="delete-btn">刪除</button>
                        </div>
                    </template>

                    <!-- 編輯模式 -->
                    <template v-else>
                        <div class="edit-form">
                            <input v-model="editForm.name" placeholder="學生姓名" />
                            <input v-model="editForm.subject" placeholder="科目" />
                            <input v-model.number="editForm.score" type="number" min="0" max="100" placeholder="分數" />
                            <div class="edit-actions">
                                <button @click="saveEdit" class="save-btn">儲存</button>
                                <button @click="cancelEdit" class="cancel-btn">取消</button>
                            </div>
                        </div>
                    </template>
                </div>
            </div>
        </div>

        <!-- 統計資訊 -->
        <div class="demo-card">
            <h4>統計資訊</h4>
            <div class="stats-grid">
                <div class="stat-item">
                    <span class="stat-label">總學生數</span>
                    <span class="stat-value">{{ students.length }}</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">平均分數</span>
                    <span class="stat-value">{{ averageScore }}</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">最高分</span>
                    <span class="stat-value">{{ highestScore }}</span>
                </div>
                <div class="stat-item">
                    <span class="stat-label">最低分</span>
                    <span class="stat-value">{{ lowestScore }}</span>
                </div>
            </div>
        </div>

        <!-- 成績分布 -->
        <div class="demo-card">
            <h4>成績分布</h4>
            <div class="grade-distribution">
                <div v-for="(count, grade) in gradeDistribution" :key="grade" class="grade-item">
                    <span class="grade-label">{{ grade }}</span>
                    <div class="grade-bar">
                        <div class="grade-fill" :style="{ width: (count / students.length * 100) + '%' }"
                            :class="getGradeClass(getGradeScore(grade))"></div>
                    </div>
                    <span class="grade-count">{{ count }} 人</span>
                </div>
            </div>
        </div>

        <!-- 科目統計 -->
        <div class="demo-card">
            <h4>科目統計</h4>
            <div class="subject-stats">
                <div v-for="(data, subject) in subjectStats" :key="subject" class="subject-item">
                    <h5>{{ subject }}</h5>
                    <p>學生數：{{ data.count }} 人</p>
                    <p>平均分：{{ data.average.toFixed(1) }} 分</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, reactive, computed } from 'vue'

// 學生資料
const students = ref([
    { id: 1, name: '王小明', subject: '數學', score: 85 },
    { id: 2, name: '李小華', subject: '英文', score: 92 },
    { id: 3, name: '張小美', subject: '數學', score: 78 }
])

// 新增學生表單
const newStudent = reactive({
    name: '',
    subject: '',
    score: 0
})

// 編輯狀態
const editingId = ref(null)
const editForm = reactive({
    name: '',
    subject: '',
    score: 0
})

// ID 計數器
let nextId = 4

// 1. addStudent 函數
const addStudent = () => {
    // 驗證資料
    if (!newStudent.name.trim() || !newStudent.subject.trim()) {
        alert('請填寫完整資料')
        return
    }

    if (newStudent.score < 0 || newStudent.score > 100) {
        alert('分數必須在 0-100 之間')
        return
    }

    // 新增學生
    const student = {
        id: nextId++,
        name: newStudent.name.trim(),
        subject: newStudent.subject.trim(),
        score: Number(newStudent.score)
    }

    students.value.push(student)

    // 重置表單
    newStudent.name = ''
    newStudent.subject = ''
    newStudent.score = 0
}

// 2. deleteStudent 函數
const deleteStudent = (id) => {
    if (confirm('確定要刪除這位學生嗎？')) {
        students.value = students.value.filter(student => student.id !== id)
    }
}

// 3. editStudent 函數
const editStudent = (student) => {
    editingId.value = student.id
    editForm.name = student.name
    editForm.subject = student.subject
    editForm.score = student.score
}

// 4. saveEdit 函數
const saveEdit = () => {
    // 驗證資料
    if (!editForm.name.trim() || !editForm.subject.trim()) {
        alert('請填寫完整資料')
        return
    }

    if (editForm.score < 0 || editForm.score > 100) {
        alert('分數必須在 0-100 之間')
        return
    }

    // 找到學生並更新
    const studentIndex = students.value.findIndex(s => s.id === editingId.value)
    if (studentIndex !== -1) {
        students.value[studentIndex] = {
            ...students.value[studentIndex],
            name: editForm.name.trim(),
            subject: editForm.subject.trim(),
            score: Number(editForm.score)
        }
    }

    // 重置編輯狀態
    cancelEdit()
}

// 5. cancelEdit 函數
const cancelEdit = () => {
    editingId.value = null
    editForm.name = ''
    editForm.subject = ''
    editForm.score = 0
}

// 6. averageScore 計算屬性
const averageScore = computed(() => {
    if (students.value.length === 0) return 0

    const total = students.value.reduce((sum, student) => sum + student.score, 0)
    return (total / students.value.length).toFixed(1)
})

// 額外的計算屬性
const highestScore = computed(() => {
    if (students.value.length === 0) return 0
    return Math.max(...students.value.map(s => s.score))
})

const lowestScore = computed(() => {
    if (students.value.length === 0) return 0
    return Math.min(...students.value.map(s => s.score))
})

const gradeDistribution = computed(() => {
    const distribution = { 'A': 0, 'B': 0, 'C': 0, 'D': 0, 'F': 0 }
    students.value.forEach(student => {
        const grade = getGrade(student.score)
        distribution[grade]++
    })
    return distribution
})

const subjectStats = computed(() => {
    const stats = {}
    students.value.forEach(student => {
        if (!stats[student.subject]) {
            stats[student.subject] = { count: 0, total: 0 }
        }
        stats[student.subject].count++
        stats[student.subject].total += student.score
    })

    Object.keys(stats).forEach(subject => {
        stats[subject].average = stats[subject].total / stats[subject].count
    })

    return stats
})

// 輔助函數
const getGrade = (score) => {
    if (score >= 90) return 'A'
    if (score >= 80) return 'B'
    if (score >= 70) return 'C'
    if (score >= 60) return 'D'
    return 'F'
}

const getGradeClass = (score) => {
    const grade = getGrade(score)
    return `grade-${grade.toLowerCase()}`
}

const getGradeScore = (grade) => {
    const scoreMap = { 'A': 95, 'B': 85, 'C': 75, 'D': 65, 'F': 50 }
    return scoreMap[grade] || 0
}
</script>

<style scoped>
.solution {
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
}

.demo-card {
    background: white;
    border: 1px solid #e9ecef;
    border-radius: 10px;
    padding: 20px;
    margin-bottom: 20px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.add-form {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
    align-items: center;
}

.add-form input {
    padding: 8px 12px;
    border: 1px solid #ced4da;
    border-radius: 5px;
    flex: 1;
    min-width: 150px;
}

.add-form button {
    padding: 8px 16px;
    background: #28a745;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

.empty-state {
    text-align: center;
    padding: 40px;
    color: #6c757d;
}

.student-list {
    display: grid;
    gap: 15px;
}

.student-card {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px;
    border: 1px solid #e9ecef;
    border-radius: 8px;
    transition: all 0.2s;
}

.student-card:hover {
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.student-card.editing {
    border-color: #007bff;
    background: #f8f9fa;
}

.student-info {
    display: flex;
    align-items: center;
    gap: 20px;
    flex: 1;
}

.student-info h5 {
    margin: 0;
    color: #495057;
    min-width: 100px;
}

.student-info p {
    margin: 0;
    color: #6c757d;
    font-size: 0.9em;
}

.grade-badge {
    padding: 4px 8px;
    border-radius: 12px;
    font-size: 0.8em;
    font-weight: bold;
    color: white;
}

.grade-a {
    background: #28a745;
}

.grade-b {
    background: #17a2b8;
}

.grade-c {
    background: #ffc107;
    color: #212529;
}

.grade-d {
    background: #fd7e14;
}

.grade-f {
    background: #dc3545;
}

.student-actions {
    display: flex;
    gap: 8px;
}

.edit-btn,
.save-btn {
    background: #007bff;
    color: white;
}

.delete-btn,
.cancel-btn {
    background: #dc3545;
    color: white;
}

.edit-form {
    display: flex;
    gap: 10px;
    align-items: center;
    flex: 1;
}

.edit-form input {
    padding: 6px 10px;
    border: 1px solid #ced4da;
    border-radius: 4px;
    flex: 1;
}

.edit-actions {
    display: flex;
    gap: 8px;
}

button {
    padding: 6px 12px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 0.9em;
    transition: opacity 0.2s;
}

button:hover {
    opacity: 0.8;
}

.stats-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 15px;
}

.stat-item {
    text-align: center;
    padding: 20px;
    background: #f8f9fa;
    border-radius: 8px;
}

.stat-label {
    display: block;
    color: #6c757d;
    font-size: 0.9em;
    margin-bottom: 8px;
}

.stat-value {
    display: block;
    font-size: 1.5em;
    font-weight: bold;
    color: #495057;
}

.grade-distribution {
    display: grid;
    gap: 10px;
}

.grade-item {
    display: flex;
    align-items: center;
    gap: 15px;
}

.grade-label {
    font-weight: bold;
    min-width: 30px;
}

.grade-bar {
    flex: 1;
    height: 20px;
    background: #e9ecef;
    border-radius: 10px;
    overflow: hidden;
}

.grade-fill {
    height: 100%;
    transition: width 0.3s ease;
}

.grade-count {
    min-width: 50px;
    text-align: right;
    font-size: 0.9em;
    color: #6c757d;
}

.subject-stats {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 15px;
}

.subject-item {
    padding: 15px;
    background: #f8f9fa;
    border-radius: 8px;
    border-left: 4px solid #007bff;
}

.subject-item h5 {
    margin: 0 0 10px 0;
    color: #495057;
}

.subject-item p {
    margin: 5px 0;
    color: #6c757d;
    font-size: 0.9em;
}
</style>
