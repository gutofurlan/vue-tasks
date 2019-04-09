<template>
  <div id="app" class="container">
    <list-tasks></list-tasks>
  </div>
</template>

<script>


import ListTasks from './components/Tasks/ListTasks'

export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }, components: {
    ListTasks
  }
}
</script>

<style>

</style>
