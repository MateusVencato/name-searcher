<template>
  <div id="app">
    <h1>Quantas pessoas existem com seu nome?</h1>
    <NameSearch/>
  </div>
</template>

<script>
import NameSearch from './components/NameSearch.vue'

export default {
  name: 'App',
  components: {
    NameSearch,
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
