<template>
  <div id="app">
    <BGMGraph />
  </div>
</template>

<script>
import BGMGraph from './components/BGMGraph.vue'
export default {
  name: 'App',
  components: {
    BGMGraph
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
