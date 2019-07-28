<template>
  <div id="app">
    <solitaire/>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import Solitaire from './components/Solitaire.vue'

export default Vue.extend({
  name: 'app',
  components: {
    Solitaire
  }
})
</script>

<style lang="scss">
html, body{
  margin: 0;
  padding: 0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 100vw;
  height: 100vh;
}
</style>
