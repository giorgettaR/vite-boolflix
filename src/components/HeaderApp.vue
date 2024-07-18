<script>
import SearchBar from './SearchBar.vue'
  
  export default {
    components: {
      SearchBar,
    }
    
  }
</script>

<template>
    <header>
        <div class="container">
        <div class="row">
            <div class="col-12 pt-4 pb-4 d-flex align-items-center justify-content-between text-center">
                <img src="/public/LogoHeader.jpg" alt="" class="logo">
                <SearchBar class="" />
            </div>
        </div>
    </div>
    </header>
</template>


<style lang="scss">

</style>