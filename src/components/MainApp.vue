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
    <section>
      <div class="container">
        <h2>Movies</h2>
      </div>
      <div class="container">
        <ul v-if="store.arrayMovies.length !== 0">
          <MovieCard v-for="movie in store.arrayMovies" :key="movie.id" :item="movie" />
        </ul>
        <p v-else>Nessun film</p>
      </div>
      <div class="container">
        <ul v-if="store.arrayTvShows.length !== 0">
          <TVShowCard v-for="tvShow in store.arrayTvShows" :key="tvShow.id" :item="tvShow"/>
        </ul>
        <p v-else>Nessun TvShows</p>
      </div>
    </section>
  </main>
</template>

<style lang="scss scoped">
</style>