<template>
  <h1>Where Have I Been?</h1>
  <MapView/>
</template>

<script>
import MapView from './components/MapView'

export default {
  name: 'App',
  components: {
    MapView
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
