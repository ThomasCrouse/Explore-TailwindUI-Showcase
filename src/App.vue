<template>

  <sidebar/>
  <img class="mx-auto" alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to the Liberty TailwindCSS Playground"/>

</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import sidebar from './components/Sidebar'

export default {
  name: 'App',
  components: {
    sidebar,
    HelloWorld
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
}
</style>
