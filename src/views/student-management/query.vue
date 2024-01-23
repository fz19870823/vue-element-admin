<template>
  <div>
    <h1>学生信息查询</h1>
    <div>
      <select v-model="searchField">
        <option value="id_card">身份证号码</option>
        <option value="name">姓名</option>
        <option value="grade">年级</option>
        <option value="class">班级</option>
      </select>
      <input v-model="searchText" placeholder="搜索...">
      <button @click="searchStudents">搜索</button>
    </div>
    <table v-if="students.length > 0">
      <thead>
        <tr>
          <th>身份证号码</th>
          <th>姓名</th>
          <th>年级</th>
          <th>班级</th>
          <th>操作</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="student in students" :key="student.id_card">
          <td>{{ student.id_card }}</td>
          <td>{{ student.name }}</td>
          <td>{{ student.grade }}</td>
          <td>{{ student.class }}</td>
          <td>
            <button @click="openModifyPage(student)">修改</button>
            <button @click="deleteStudent(student)">删除</button>
          </td>
        </tr>
      </tbody>
    </table>
    <p v-else>没有学生信息</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'StudentQuery',
  data() {
    return {
      students: [],
      searchField: 'id_card',
      searchText: ''
    }
  },
  created() {
    this.fetchStudents()
  },
  methods: {
    fetchStudents() {
      axios.post('https:://zongping.nxjtxx.tk:8889/submit.php', {
        action: 'query',
        limit: 20
      })
        .then(response => {
          this.students = response.data
        })
    },
    searchStudents() {
      if (this.searchText === '') {
        this.fetchStudents()
      } else {
        axios.post('https:://zongping.nxjtxx.tk:8889/submit.php', {
          action: 'search',
          field: this.searchField,
          text: this.searchText
        })
          .then(response => {
            this.students = response.data
          })
      }
    },
    openModifyPage(student) {
      this.$router.push({ name: 'ModifyStudent', params: { student: student }})
    },
    deleteStudent(student) {
      // ...
    }
  }
}
</script>

<style scoped>
/* Your styles go here */
</style>
