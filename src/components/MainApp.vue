<script>
import { store } from '../store';
import MovieCard from './MovieCard.vue';
import TVShowCard from './TVShowCard.vue';


export default {
  data(){
    return {
        store: store,
        visibleMoviesI: 5,
        visibleTVShowsI: 5
    }
  },
  components: {
    MovieCard,
    TVShowCard
  },
  methods: {
    visibleMovies(i){
      let visible = []
      for (let i = 0; i < this.visibleMoviesI; i++){
        visible.push(this.store.arrayMovies[i])
      }
      console.log()
      return visible
    },
    visibleTVShows(){
      let visible = []
      for (let i = 0; i < this.visibleTVShowsI; i++){
        visible.push(this.store.arrayTvShows[i])
      }
      console.log()
      return visible
    }
  }
  
}
</script>

<template>

<main>
  <div class="container text-white">
    <div class="row">
      <div class="movies col-12">
        <div class="row">
          <h3 class="col-12 title">Movies</h3>
          <div class="col-12 results d-flex flex-row flex-wrap"
            v-if="store.arrayMovies.length !== 0">
            <MovieCard v-for="movie in (visibleMovies(visibleMoviesI))" :key="movie.id" :item="movie" />
            <button class="btn"></button>
          </div>
          <p v-else>Nessun film trovato</p>
        </div>
      </div>
      <div class="tvShows col-12">
        <div class="row">
          <h3 class="col-12 title">TV-Shows</h3>
          <div class="col-12 results d-flex flex-row flex-wrap"
            v-if="store.arrayTvShows.length !== 0">
            <MovieCard v-for="tvShow in visibleTVShows(visibleTVShowsI)" :key="tvShow.id" :item="tvShow" />
          </div>
          <p v-else>Nessun tv-Show trovato</p>
        </div>
      </div>
    </div>
  </div>
</main>
</template>

<style lang="scss scoped">
</style>