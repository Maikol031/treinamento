<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="WEL N COMEU NINGUEM"/>
  <HelloMaikol/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import HelloMaikol from './components/HelloMaikol.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    HelloMaikol
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
