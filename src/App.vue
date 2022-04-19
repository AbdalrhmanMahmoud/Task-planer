<template>
<Nav />
  <router-view />

</template>

<script>
import Nav from '@/components/nav.vue'

export default {
  components:{Nav}
  
}
</script>
<style lang="scss">
body {
  background-color: #ddd;
}
body #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 600px;
  margin: 0 auto;
}


</style>
