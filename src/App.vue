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
    },
    beforeCreate: function() {
        document.body.className = 'classForBackgroundBody';
    },
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

.classForBackgroundBody {
    background: linear-gradient( #bbb, transparent 1px), linear-gradient( 90deg, #bbb, transparent 1px);
    background-size: 15px 15px;
    background-position: center center;
}
</style>
