<template>
  <Navbar/>
  <router-view/>
</template>

<script>
import Navbar from './components/Navbar';
export default {
  components: { Navbar },
}
</script>
<style>
body{
  background-color: #f2f2f2;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #555;
  max-width: 600px;
  margin: 0 auto;
}
</style>
