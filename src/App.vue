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
  overflow: hidden;
}

#app {
  font-family: Helvetica, Arial, sans-serif;
  text-align: center;
}

.decor {
  position: relative;
  width: 100vw;
  height: 50px;
  background-color: rgba(0, 0, 0, 0.8);
  top: 100%;
  transform: translateY(-100%);
}

.link {
  width: 64px;
  height: 46px;
  position: relative;
  border-bottom: 4px solid #008000;
  margin-left: 10px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
</style>
