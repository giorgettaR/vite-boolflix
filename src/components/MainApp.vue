<script>
import axios from 'axios'
import { store } from '../store';
import MovieCard from './MovieCard.vue';
import TVShowCard from './TVShowCard.vue';
import { onMounted } from 'vue';


export default {
  setup(){
    onMounted( () => {
      axios.get(`https://api.themoviedb.org/3/discover/movie?api_key=952819b1623493b0abb662f846bd0331`).then((res) => {
        store.arrayMovies  = res.data.results
      });
      axios.get(`https://api.themoviedb.org/3/discover/tv?api_key=952819b1623493b0abb662f846bd0331`).then((res) => {
        store.arrayTVShows  = res.data.results
      })
    })
  },
  data(){
    return {
        store: store,
        posterAmount: 5,
        visibleMoviesI: 0,
        visibleTVShowsI: 0
    }
  },
  components: {
    MovieCard,
    TVShowCard
  },
  methods: {
    visibleMovies(){
      let visible = []
      for (let i = this.visibleMoviesI; i < (this.visibleMoviesI + this.posterAmount ); i++){
        visible.push(this.store.arrayMovies[i])
      }
      console.log()
      return visible
    },
    leftSlideMovies(){
      if (this.visibleMoviesI > 0) {
        this.visibleMoviesI--
      }
    },
    rightSlideMovies(){
      if (this.visibleMoviesI < store.arrayMovies.length) {
        this.visibleMoviesI++
      }
    },
    visibleTVShows(){
      let visible = []
      for (let i = this.visibleTVShowsI; i < (this.visibleTVShowsI + this.posterAmount); i++){
        visible.push(this.store.arrayTVShows[i])
      }
      return visible
    },   
    leftSlideTVShows(){
      if (this.visibleTVShowsI > 0) {
        this.visibleTVShowsI--
      }
    },
    rightSlideTVShows(){
      if (this.visibleTVShowsI < store.arrayTVShows.length) {
        this.visibleTVShowsI++
      }
    },
    clickone(){
      console.log(this.visibleMoviesI)
      console.log(store.arrayMovies.length + this.posterAmount)
    }

  },
  computed: {
    disableCheckLeftSlideMovies() {
      if (this.visibleMoviesI != 0) {
        return false
      } else {
        return true
      }
    },
    disableCheckRightSlideMovies() {
      if (this.visibleMoviesI != (store.arrayMovies.length - this.posterAmount)) {
        return false
      } else {
        return true
      }
    },
    disableCheckLeftSlideTVShows() {
      if (this.visibleTVShowsI != 0) {
        return false
      } else {
        return true
      }
    },
    disableCheckRightSlideTVShows() {
      if (this.visibleTVShowsI != (store.arrayTVShows.length - this.posterAmount)) {
        return false
      } else {
        return true
      }
    },
  }
};


  
</script>

<template>

<main>
  <div class="container text-white">
    <div class="row">
      <div class="movies pt-3 pb-5 col-12">
        <div class="row">
          <h3 class="col-12 pb-5 title">Movies</h3>
          <div class="col-12 results d-flex flex-row justify-content-between align-items-center"
            v-if="store.arrayMovies.length !== 0">
            <button class="fw-bold slider" :disabled="disableCheckLeftSlideMovies" @click="[leftSlideMovies(), clickone()]"><</button>
            <MovieCard v-for="movie in (visibleMovies())" :key="movie.id" :item="movie"/>
            <button class="fw-bold slider" :disabled="disableCheckRightSlideMovies" @click="[rightSlideMovies(), clickone()]">></button>
          </div>
          <p v-else>No results found for your search</p>
        </div>
      </div>
      <div class="tvShows pt-3 pb-5 col-12">
        <div class="row">
          <h3 class="col-12 pb-5 title">TV-Shows</h3>
          <div class="col-12 results d-flex flex-row flex-wrap justify-content-between align-items-center"
            v-if="store.arrayTVShows.length !== 0">
             <button class="slider" :disabled="disableCheckLeftSlideTVShows" @click="leftSlideTVShows()"><</button>
            <TVShowCard v-for="tvShow in visibleTVShows(posterAmount)" :key="tvShow.id" :item="tvShow"  />
            <button class="slider" :disabled="disableCheckRightSlideTVShows" @click="rightSlideTVShows()">></button>
          </div>
          <p v-else>No results found for your search</p>
        </div>
      </div>
    </div>
  </div>
</main>
</template>

<style lang="scss scoped">
</style>