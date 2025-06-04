<template>
    <div class="student-grade-practice">
        <h2>🎓 學生成績管理 - Computed 計算屬性練習</h2>
        <p class="route-info">📍 路徑：/ComputedSamples/StudentGradePractice.vue</p>
        <p class="description">
            📝 <strong>練習目標：</strong>學習使用 computed 計算屬性來處理成績計算、等級評定、統計分析
        </p>

        <div class="demo-section">
            <h3>🎯 練習任務</h3>
            <div class="task-list">
                <div class="task-item">
                    <span>✅ 1. 計算學生平均分數</span>
                </div>
                <div class="task-item">
                    <span>✅ 2. 根據分數自動評定等級</span>
                </div>
                <div class="task-item">
                    <span>✅ 3. 統計各等級人數</span>
                </div>
                <div class="task-item">
                    <span>✅ 4. 計算班級整體統計</span>
                </div>
            </div>
        </div>

        <div class="demo-section">
            <h3>📊 新增學生成績</h3>
            <div class="input-form">
                <input v-model="newStudent.name" placeholder="學生姓名" class="input-field">
                <input v-model.number="newStudent.math" type="number" placeholder="數學成績 (0-100)" class="input-field"
                    min="0" max="100">
                <input v-model.number="newStudent.english" type="number" placeholder="英語成績 (0-100)" class="input-field"
                    min="0" max="100">
                <input v-model.number="newStudent.science" type="number" placeholder="科學成績 (0-100)" class="input-field"
                    min="0" max="100">
                <button @click="addStudent" class="btn btn-primary">
                    新增學生
                </button>
            </div>
        </div>

        <div class="demo-section">
            <h3>👥 學生成績列表</h3>
            <div v-if="students.length === 0" class="empty-list">
                還沒有學生資料，請先新增學生成績
            </div>
            <div v-else class="student-list">
                <div v-for="student in studentsWithGrades" :key="student.id" class="student-card"
                    :class="getGradeClass(student.grade)">
                    <div class="student-header">
                        <h4>{{ student.name }}</h4>
                        <span class="grade-badge">{{ student.grade }}</span>
                    </div>
                    <div class="student-scores">
                        <div class="score-item">
                            <span>數學：</span>
                            <span>{{ student.math }}</span>
                        </div>
                        <div class="score-item">
                            <span>英語：</span>
                            <span>{{ student.english }}</span>
                        </div>
                        <div class="score-item">
                            <span>科學：</span>
                            <span>{{ student.science }}</span>
                        </div>
                    </div>
                    <div class="student-average">
                        平均分：{{ student.average.toFixed(1) }}
                    </div>
                    <button @click="removeStudent(student.id)" class="btn btn-danger btn-sm">
                        刪除
                    </button>
                </div>
            </div>
        </div>

        <div class="demo-section" v-if="students.length > 0">
            <h3>📈 班級統計</h3>
            <div class="statistics-grid">
                <div class="stat-card">
                    <div class="stat-number">{{ classAverage.toFixed(1) }}</div>
                    <div class="stat-label">班級平均分</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">{{ highestScore }}</div>
                    <div class="stat-label">最高分</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">{{ lowestScore }}</div>
                    <div class="stat-label">最低分</div>
                </div>
                <div class="stat-card">
                    <div class="stat-number">{{ passRate.toFixed(1) }}%</div>
                    <div class="stat-label">及格率</div>
                </div>
            </div>

            <div class="grade-distribution">
                <h4>📊 等級分布</h4>
                <div class="grade-bars">
                    <div v-for="(count, grade) in gradeDistribution" :key="grade" class="grade-bar">
                        <div class="grade-label">{{ grade }} ({{ count }}人)</div>
                        <div class="bar-container">
                            <div class="bar-fill" :class="getGradeClass(grade)"
                                :style="{ width: getBarWidth(count) + '%' }"></div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <div class="code-example">
            <h4>💻 關鍵代碼</h4>
            <pre v-pre><code>// 使用 computed 計算學生等級和平均分
const studentsWithGrades = computed(() =&gt; {
  return students.value.map(student =&gt; {
    const average = (student.math + student.english + student.science) / 3
    return {
      ...student,
      average,
      grade: getGrade(average)
    }
  })
})

// 計算班級平均分
const classAverage = computed(() =&gt; {
  if (students.value.length === 0) return 0
  const total = studentsWithGrades.value.reduce((sum, student) =&gt; {
    return sum + student.average
  }, 0)
  return total / studentsWithGrades.value.length
})

// 等級分布統計
const gradeDistribution = computed(() =&gt; {
  const distribution = { 'A': 0, 'B': 0, 'C': 0, 'D': 0, 'F': 0 }
  studentsWithGrades.value.forEach(student =&gt; {
    distribution[student.grade]++
  })
  return distribution
})</code></pre>
        </div>
    </div>
</template>

<script setup>
import { ref, computed } from 'vue'

// 學生數據
const students = ref([
    { id: 1, name: '小明', math: 85, english: 78, science: 92 },
    { id: 2, name: '小華', math: 76, english: 88, science: 74 },
    { id: 3, name: '小美', math: 94, english: 91, science: 89 }
])

// 新學生表單
const newStudent = ref({
    name: '',
    math: 0,
    english: 0,
    science: 0
})

// 計算學生等級和平均分
const studentsWithGrades = computed(() => {
    return students.value.map(student => {
        const average = (student.math + student.english + student.science) / 3
        return {
            ...student,
            average,
            grade: getGrade(average)
        }
    })
})

// 計算班級平均分
const classAverage = computed(() => {
    if (students.value.length === 0) return 0
    const total = studentsWithGrades.value.reduce((sum, student) => {
        return sum + student.average
    }, 0)
    return total / studentsWithGrades.value.length
})

// 計算最高分
const highestScore = computed(() => {
    if (students.value.length === 0) return 0
    return Math.max(...studentsWithGrades.value.map(s => s.average))
})

// 計算最低分
const lowestScore = computed(() => {
    if (students.value.length === 0) return 0
    return Math.min(...studentsWithGrades.value.map(s => s.average))
})

// 計算及格率
const passRate = computed(() => {
    if (students.value.length === 0) return 0
    const passCount = studentsWithGrades.value.filter(s => s.average >= 60).length
    return (passCount / studentsWithGrades.value.length) * 100
})

// 等級分布統計
const gradeDistribution = computed(() => {
    const distribution = { 'A': 0, 'B': 0, 'C': 0, 'D': 0, 'F': 0 }
    studentsWithGrades.value.forEach(student => {
        distribution[student.grade]++
    })
    return distribution
})

// 根據分數獲取等級
const getGrade = (score) => {
    if (score >= 90) return 'A'
    if (score >= 80) return 'B'
    if (score >= 70) return 'C'
    if (score >= 60) return 'D'
    return 'F'
}

// 獲取等級對應的CSS類
const getGradeClass = (grade) => {
    const classes = {
        'A': 'grade-a',
        'B': 'grade-b',
        'C': 'grade-c',
        'D': 'grade-d',
        'F': 'grade-f'
    }
    return classes[grade] || ''
}

// 計算長條圖寬度
const getBarWidth = (count) => {
    const max = Math.max(...Object.values(gradeDistribution.value))
    return max === 0 ? 0 : (count / max) * 100
}

// 新增學生
const addStudent = () => {
    if (!newStudent.value.name.trim()) {
        alert('請輸入學生姓名')
        return
    }

    if (newStudent.value.math < 0 || newStudent.value.math > 100 ||
        newStudent.value.english < 0 || newStudent.value.english > 100 ||
        newStudent.value.science < 0 || newStudent.value.science > 100) {
        alert('成績必須在 0-100 之間')
        return
    }

    students.value.push({
        id: Date.now(),
        name: newStudent.value.name,
        math: newStudent.value.math,
        english: newStudent.value.english,
        science: newStudent.value.science
    })

    // 清空表單
    newStudent.value = {
        name: '',
        math: 0,
        english: 0,
        science: 0
    }
}

// 刪除學生
const removeStudent = (studentId) => {
    const index = students.value.findIndex(s => s.id === studentId)
    if (index > -1) {
        students.value.splice(index, 1)
    }
}
</script>

<style scoped>
.input-form {
    display: flex;
    gap: 1rem;
    flex-wrap: wrap;
    margin: 1rem 0;
}

.input-field {
    flex: 1;
    min-width: 150px;
}

.student-list {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 1rem;
    margin: 1rem 0;
}

.student-card {
    border: 1px solid #ddd;
    border-radius: 8px;
    padding: 1rem;
    background: white;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.student-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1rem;
}

.grade-badge {
    padding: 0.25rem 0.5rem;
    border-radius: 4px;
    font-weight: bold;
    color: white;
}

.grade-a .grade-badge,
.grade-a .bar-fill {
    background-color: #28a745;
}

.grade-b .grade-badge,
.grade-b .bar-fill {
    background-color: #17a2b8;
}

.grade-c .grade-badge,
.grade-c .bar-fill {
    background-color: #ffc107;
    color: #000;
}

.grade-d .grade-badge,
.grade-d .bar-fill {
    background-color: #fd7e14;
}

.grade-f .grade-badge,
.grade-f .bar-fill {
    background-color: #dc3545;
}

.student-scores {
    display: flex;
    justify-content: space-between;
    margin-bottom: 1rem;
}

.score-item {
    display: flex;
    flex-direction: column;
    text-align: center;
}

.student-average {
    font-weight: bold;
    font-size: 1.1rem;
    margin-bottom: 1rem;
    text-align: center;
}

.statistics-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
    margin: 1rem 0;
}

.stat-card {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    color: white;
    padding: 1.5rem;
    border-radius: 8px;
    text-align: center;
}

.stat-number {
    font-size: 2rem;
    font-weight: bold;
    margin-bottom: 0.5rem;
}

.stat-label {
    font-size: 0.9rem;
    opacity: 0.9;
}

.grade-distribution {
    background: #f8f9fa;
    padding: 1rem;
    border-radius: 8px;
    margin-top: 1rem;
}

.grade-bars {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}

.grade-bar {
    display: flex;
    align-items: center;
    gap: 1rem;
}

.grade-label {
    min-width: 80px;
    font-weight: bold;
}

.bar-container {
    flex: 1;
    height: 25px;
    background: #e9ecef;
    border-radius: 12px;
    overflow: hidden;
}

.bar-fill {
    height: 100%;
    border-radius: 12px;
    transition: width 0.3s ease;
}

.task-list {
    background: #f8f9fa;
    padding: 1rem;
    border-radius: 8px;
    margin: 1rem 0;
}

.task-item {
    padding: 0.5rem 0;
    color: #28a745;
}

.empty-list {
    text-align: center;
    padding: 2rem;
    color: #666;
    font-style: italic;
}
</style>
