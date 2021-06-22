<template>
  <div id="app">
    <mainscreen />
  </div>
</template>

<script>
import mainscreen from './components/mainscreen.vue'

export default {
  name: 'App',
  components: {
    mainscreen
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
  padding: 20px;

}
</style>
