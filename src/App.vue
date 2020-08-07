<template>
  <div id="app">
    <MyTable />
  </div>
</template>

<script>
import MyTable from './components/MyTable.vue'

export default {
  components: {
      MyTable
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
