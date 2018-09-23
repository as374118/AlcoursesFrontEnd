<template>
    <div>
        <h1>This is courses list</h1>
        <button @click="loadCourses">Fetch please</button>
        <br>
        {{ courses }}
    </div>
</template>

<script>
import {HTTP} from '../http-common'

export default {
  name: 'CoursesList',
  data: function () {
   return {
       courses: []
   }
  },
  methods: {
      logIn: function () {
          var vm = this

          HTTP.post('spUserAuthenticate', {
              '@username': 'test',
              '@password': 'test'
          }).then(function (res) {
              let token = res.data.recordset[0].userToken
              vm.token = token
              console.log(token)
          }).catch(function (err) {
              console.log(err)
              console.log('Fail')
          })
      },
      isAuthenticated: function () {
          const res = Boolean(this.token)
          console.log(res)

          return res
      },
      loadCourses: function () {
          let vm = this

          if (!this.isAuthenticated()) {
              this.logIn();
          } else {
              console.log('Requesting for courses')
              HTTP.post('spGetCourses', {
                  '@userToken': vm.token,
                  '@canRead': true,
                  '@canModify': true
              }).then(function (res) {
                  let courses = res.data.recordset[0]
                  vm.courses = courses
              }).catch(function (err) {
                  console.log('Fail while geetin courses')
              })
          }
      }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
