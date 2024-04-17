<script>
import axios from 'axios'
import { store } from '../store.js'

export default {
    data(){
        return {
            searchValue: ''
        }
    },
    methods: {
        GetMovies(){
            if (this.searchValue != '') {
                axios.get(`https://api.themoviedb.org/3/search/movie?api_key=952819b1623493b0abb662f846bd0331&query=${this.searchValue}`).then((res) => {
                store.arrayMovies  = res.data.results
                console.log(store.arrayMovies)
                })
            }
        }
    }
}
</script>

<template>
    <div class="container">
        <input v-model.trim="searchValue" type="text" placeholder="type something">
        <button @click="GetMovies"> Search </button>
    </div>
</template>

<style lang="scss scoped">
</style>