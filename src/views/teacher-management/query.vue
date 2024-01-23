<template>
  <div>
    <h1>教师信息查询</h1>
    <div>
      <select v-model="searchField">
        <option value="id_card">身份证号码</option>
        <option value="name">姓名</option>
        <option value="username">用户名</option>
      </select>
      <input v-model="searchText" placeholder="搜索...">
      <button @click="searchTeachers">搜索</button>
    </div>
    <table v-if="teachers.length > 0">
      <thead>
        <tr>
          <th>身份证号码</th>
          <th>姓名</th>
          <th>用户名</th>
          <th>密码</th>
          <th>操作</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="teacher in teachers" :key="teacher.id_card">
          <td>{{ teacher.id_card }}</td>
          <td>{{ teacher.name }}</td>
          <td>{{ teacher.username }}</td>
          <td>******</td>
          <td>
            <button @click="openModifyPage(teacher)">修改</button>
            <button @click="deleteTeacher(teacher)">删除</button>
          </td>
        </tr>
      </tbody>
    </table>
    <p v-else>没有教师信息</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'TeacherQuery',
  data() {
    return {
      teachers: [],
      searchField: 'id_card',
      searchText: ''
    }
  },
  created() {
    this.fetchTeachers()
  },
  methods: {
    fetchTeachers() {
      axios.post('http://your-server.com/path-to-your-php-script.php', {
        action: 'query',
        limit: 20
      })
        .then(response => {
          this.teachers = response.data
        })
    },
    searchTeachers() {
      // ...
    },
    openModifyPage(teacher) {
      // ...
    },
    deleteTeacher(teacher) {
      // ...
    }
  }
}
</script>

  <style scoped>
  /* Your styles go here */
  </style>
