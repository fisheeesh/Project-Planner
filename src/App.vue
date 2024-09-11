<template>
  <NavBar></NavBar>
  <router-view/>
</template>
<script>
import NavBar from './components/NavBar'
export default {
  components: { NavBar },
  
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 600px;
  /* background-color: red; */
  margin: 0 auto;
  color: #2c3e50;
}
body{
  background-color: #eee;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
</style>
