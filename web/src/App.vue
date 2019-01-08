<template>
  <div id="app">
    <img src="./assets/logo.png">
    <AnimationSocket/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld'
// import Home from './components/Home'
import AnimationSocket from './components/AnimationSocket'

export default {
  name: 'app',
  components: {
    AnimationSocket
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
