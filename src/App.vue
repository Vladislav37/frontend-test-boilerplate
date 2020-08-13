<template>
  <div id="app">
    <BaseTable />
  </div>
</template>

<script>
import BaseTable from './components/BaseTable.vue'

export default {
    components: {
        BaseTable
    },
    beforeCreate: function() {
        document.body.className = 'class-for-background-body';
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

.class-for-background-body {
    background: linear-gradient( #bbb, transparent 1px), linear-gradient( 90deg, #bbb, transparent 1px);
    background-size: 15px 15px;
    background-position: center center;
}
</style>
