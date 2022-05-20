<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <BuildingList msg="The City of Futurpruf cell phone coverage"/>
  </div>
</template>

<script>
import BuildingList from './components/BuildingList.vue'


export default {
  name: 'App',
  components: {
    BuildingList
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
