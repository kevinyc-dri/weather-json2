// App.vue

<template>
  <div id="app">
    <Weather />
    <!-- <Demo title="kevin" :names="['Kevin', 'John', 'Sally']"/> -->

  </div>
</template>

<script>
import Weather from './components/Weather.vue'
// import Demo from './components/Demo.vue'

export default {
  name: 'app',
  components: {
    Weather,
    // Demo,
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
  background-color: lightgrey;
}
</style>