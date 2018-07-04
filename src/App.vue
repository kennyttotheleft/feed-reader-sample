<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style lang="scss">
@import "../node_modules/bulma/bulma.sass"; /** Add bluma */
html {
  height: 100%;
}
body{
  height: 100%;
  margin: 0;
  background-color: silver;
  text-align: center;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: block;
  color: #2c3e50;
  background-color: white;
  margin: 0 auto;
  min-width: 320px;
  margin: 0 auto;
  height: 100%;
}
</style>
