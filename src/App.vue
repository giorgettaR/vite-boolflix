
<script>
import MainApp from './components/MainApp.vue'
import SearchBar from './components/SearchBar.vue'
  
  export default {
    components: {
      MainApp,
      SearchBar,
    }
    
  }
</script>

<template>
  <SearchBar />
  <MainApp />
</template>


<style lang="scss">
@use './style/general';

</style>