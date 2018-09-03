<template>
  <div id="app">
    <Calculator></Calculator>
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'

export default {
    name: 'app',
    components: {
        Calculator
    }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
  position: relative;
  height: 100vh;
  width: 100vw;
}

#app {
  font-family: Helvetica, Arial, sans-serif;
  text-align: center;
}
</style>
