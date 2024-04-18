
<script>
import MainApp from './components/MainApp.vue'
import HeaderApp from './components/HeaderApp.vue'
  
  export default {
    components: {
      MainApp,
      HeaderApp,
    }
    
  }
</script>

<template>
  <HeaderApp />
  <MainApp />
</template>


<style lang="scss">
@use './style/general';

</style>