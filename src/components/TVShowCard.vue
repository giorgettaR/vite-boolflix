<script>
  export default {
    data(){
        return {
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
    props: {
      item: {
        type: Object,
        required: true
      }
    },
    methods: {
      fetchInfo(){
            if (this.gotInfo == false){
              axios.get(`https://api.themoviedb.org/3/tv/${this.item.id}/credits?api_key=952819b1623493b0abb662f846bd0331`).then((res) => {
              this.currentCast = res.data
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
        getVote() {
          return this.item.vote_average.toFixed(1)
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
  <div class="card text-white bg-black">
    <img v-if="item.poster_path != null" class="poster h-100 w-100 z-2" :src="getPosterPath(item.poster_path)" alt="">
    <img v-else class="poster h-100 w-100 z-2 p-5" src="https://ouch-cdn2.icons8.com/oUSOvdU3-qOpsDEsyA3XdoROq4gPnbYncCh9XbUhse4/rs:fit:368:670/czM6Ly9pY29uczgu/b3VjaC1wcm9kLmFz/c2V0cy9zdmcvNDI5/L2ZlOGJhYjAyLTZi/OWEtNDJkYy1iZjA0/LTA2M2FhODBiYjMw/Mi5zdmc.png" alt="">
    <div class="info h-100 w-100 p-3 z-3">
      <h6 class="card-title fw-bold fs-5">{{ item.original_name }}</h6>
      <p>Primo Episodio: {{ item.first_air_date }}</p>
      <p v-if="areNamesEquals == false">Titolo originale: {{ item.original_title }}</p>
      <p>Lingua Originale: {{ item.original_language }}</p>
      <p>Voto: {{ getVote() }}</p>
      <p>
        <font-awesome-icon v-for="n in getStarVote(item.vote_average)" :key="n" :icon="['fas', 'star']" />
        <font-awesome-icon v-for="n in 5-getStarVote(item.vote_average)" :key="n" :icon="['far', 'star']" />
      </p>
      <button class="btn btn-outline-secondary" @click="fetchInfo()"> INFO </button>
      <img class="lang" :src="getImgPath(item.original_language)" alt="">
    </div>
  </div>
</template>

<style lang="scss scoped">

</style>