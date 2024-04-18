<script>
import { store } from '../store';
import MovieCard from './MovieCard.vue';
import TVShowCard from './TVShowCard.vue';


export default {
  data(){
    return {
        store: store
    }
  },
  components: {
    MovieCard,
    TVShowCard
  },
  
}
</script>

<template>

<main>
  <div class="container">
    <div class="row">
      <div class="movies col-12">
        <h3>Movies</h3>
        <ul class="d-flex flex-row flex-wrap"
          v-if="store.arrayMovies.length !== 0">
          <MovieCard v-for="movie in store.arrayMovies" :key="movie.id" :item="movie" />
        </ul>
        <p v-else>Nessun film</p>
      </div>
      <div class="col-12">
        <h3>TV Shows</h3>

      </div>

    </div>
  </div>
</main>
 

    <section>
      <div class="container">
        <h2>Movies</h2>
      </div>
      <div class="container">
        
      </div>
      <div class="container">
        <ul v-if="store.arrayTvShows.length !== 0">
          <TVShowCard v-for="tvShow in store.arrayTvShows" :key="tvShow.id" :item="tvShow"/>
        </ul>
        <p v-else>Nessun TvShows</p>
      </div>
    </section>
</template>

<style lang="scss scoped">
</style>