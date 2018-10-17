<template>
  <div id="app">
    <Cliente/>
    
    <notifications group="foo" /> 
  </div>
</template>

<script>
import Cliente from './components/Cliente.vue'
import Painel from './components/Painel.vue'


export default {
  name: 'app',
  components: {
    Cliente,
    Painel
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
