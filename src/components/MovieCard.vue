
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
            showInfo: false,
            gotInfo: false,
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
        fetchInfo(movie){
            if (this.gotInfo == false){
              axios.get(`https://api.themoviedb.org/3/movie/${this.item.id}/credits?api_key=952819b1623493b0abb662f846bd0331`).then((res) => {
              this.currentCast = res.data.cast
              this.currentCast.length = 5
              })
              this.gotInfo = true
            }
            if (this.showInfo){
              this.showInfo = true
            } else {
              this.showInfo = !this.showInfo
            }
            console.log(this.currentCast)
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
    },
    computed: {
      areNamesEquals() {
        if (this.item.title == this.item.original_title) {
          return true
        } else {
          return false
        }
      }
    }
  }
</script>

<template>
  <div class="card text-white bg-black p-2">
    <img class="poster" :src="getPosterPath(item.poster_path)" alt="">

    <div class="card-body p-3">

      <h6 class="card-title">{{ item.title }}</h6>
        <img class="lang" :src="getImgPath(item.original_language)" alt="">
        <p v-if="areNamesEquals == false">Titolo originale: {{ item.original_title }}</p>
        <p>
          Lingua Originale: {{ item.original_language }}
        </p>
        <p>Voto: {{ item.vote_average }}</p>
        <p>
          <font-awesome-icon v-for="n in getStarVote(item.vote_average)" :key="n" :icon="['fas', 'star']" />
          <font-awesome-icon v-for="n in 5-getStarVote(item.vote_average)" :key="n" :icon="['far', 'star']" />
        </p>
        <button class="btn btn-outline-secondary" @click="fetchInfo(item)"> INFO </button>
      <!-- <ul v-if="(this.showInfo == true)">
        <li v-for="actor in currentCast"> {{ actor.name }}</li>
      </ul> -->
    </div>
  </div>
</template>

<style lang="scss scoped">

</style>