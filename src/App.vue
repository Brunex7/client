<template>
  <HeaderComp />
  <MetodoPagos />
</template>

<script>
import HeaderComp from './components/HeaderComp.vue'
import MetodoPagos from './components/MetodoPagos.vue'

export default {
  name: 'App',
  components: {
    HeaderComp,
    MetodoPagos

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #3D3D3D;
}
</style>
