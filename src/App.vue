<template>
  <div id="app">
    <formAPI/>
  </div>
</template>

<script>
import formAPI from './components/formAPI'

export default {
  name: 'app',
  components: {
    formAPI
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
