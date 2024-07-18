<script>
import axios from 'axios'
import { store } from '../store.js'

export default {
    data(){
        return {
            searchValue:'',
        }
    },
    methods: {
        FetchSearch(){
            if (this.searchValue != '') {
                axios.get(`https://api.themoviedb.org/3/search/movie?api_key=952819b1623493b0abb662f846bd0331&query=${this.searchValue}`).then((res) => {
                store.arrayMovies  = res.data.results
                console.log(store.arrayMovies)
                })
                axios.get(`https://api.themoviedb.org/3/search/tv?api_key=952819b1623493b0abb662f846bd0331&query=${this.searchValue}`).then((res) =>{
                store.arrayTvShows  = res.data.results
                console.log(store.arrayTvShows)
                })
            }
        }
    },
    computed: {
        disableCheck(){
            if (this.searchValue != '') {
                return false
            } else {
                return true
            }
        }
    }
}
</script>

<template>
    <div class="d-flex justify-content-between">
        <input class="d-block p-1 m-1 me-3" v-model.trim="searchValue" type="text" placeholder="Type something">
        <button class="btn btn-light mt-1 mb-1" :disabled="disableCheck" @click="FetchSearch"> Search </button>
    </div>
</template>

<style lang="scss scoped">
</style>