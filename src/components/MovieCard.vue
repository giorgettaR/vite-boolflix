
<script>
import axios from 'axios'
import { store } from '../store';


  export default {
    props: {
      item: {
        type: Object,
        required: true
      }
    },
    data(){
        return {
            showGeners: Boolean,
            showCast: false,
            gotCast: false,
            currentCast: [],
            flags: [
                {
                    language: 'en',
                    flag: '/public/flags/english.png'
                },
                {
                    language: 'it',
                    flag: '/public/flags/italian.png'
                },
                {
                    language: 'fr',
                    flag: '/public/flags/french.png'
                },
                {
                    language: 'es',
                    flag: '/public/flags/spanish.png'
                },
            ]
        }
    },
    methods: {
        fetchCast(movie){
            if (!this.gotCast){
                console.log(movie)
                axios.get(`https://api.themoviedb.org/3/movie/24115/credits?api_key=952819b1623493b0abb662f846bd0331`).then((res) => {
                let cast = res.data.cast
                cast.length = 5
                this.currentCast = cast
                })
                this.gotCast = !this.gotCast
                this.showcast = !this.showCast
            } else {
                this.showcast = !this.showCast
            }
        },
        getImgPath(abbreviation) {
            let lang =this.flags.find((country) => country.language == abbreviation)
            if (lang !== undefined) {
                return lang.flag
            }
        },
        getStarVote(vote_av) {
            return Math.floor( vote_av / 2 )
        },
        getPosterPath(path) {
            return `https://image.tmdb.org/t/p/w342${path}`
        }
    }
  }
</script>

<template>
  <li class="card text-white bg-black p-2">
    <img class="poster" :src="getPosterPath(item.poster_path)" alt="">

    <div class="card-body">
      <h4 class="card-title">{{ item.title }}</h4>

      <p v-if="areNamesEquals">Titolo originale: {{ item.original_title }}</p>
      <p>Lingua Originale:{{ item.original_language }}</p>
      <p>Voto: {{ item.vote_average }}</p>
      <img :src="getImgPath(item.original_language)" alt="">
      <p>
        <font-awesome-icon v-for="n in getStarVote(item.vote_average)" :key="n" :icon="['fas', 'star']" />
        <font-awesome-icon v-for="n in 5-getStarVote(item.vote_average)" :key="n" :icon="['far', 'star']" />
      </p>
      <button @click="fetchCast(item)"> CAST </button>
      <ul v-if="(!this.showCast)">
        <li v-for="actor in currentCast">{{ actor.name }}</li>
      </ul>
    </div>
  </li>
</template>

<style lang="scss scoped">

</style>