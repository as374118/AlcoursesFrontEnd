<template>
  <div id="app">
    <NavigationPanel title="Alcourses-in building"/>

    <CoursesList/>
  </div>
</template>

<script>

import CoursesList from './components/CoursesList.vue'
import NavigationPanel from './components/NavigationPanel.vue'

export default {
  name: 'app',
  components: {
    NavigationPanel,
    CoursesList
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
