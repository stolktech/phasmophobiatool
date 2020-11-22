<template>
  <div id="app">
    <ClueTool />
  </div>
</template>

<script>
import ClueTool from './components/ClueTool.vue'

export default {
  name: 'App',
  components: {
    ClueTool
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: rgb(225,225,255);
  min-height: 100vh;
  width: 100vw;
}
body {
  margin: 0;
  padding: 0;
}
</style>
