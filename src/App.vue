<template>
  <div id="app">
    <calculation></calculation>
  </div>
</template>

<script>
import Calculation from './components/Calculation'

export default {
  name: 'app',
  components: {
    Calculation
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
