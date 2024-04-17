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
  <li class="card">
    <div class="card-body">
      <p>Titolo: {{ item.original_name }}</p>
      <p>Primo Episodio: {{ item.first_air_date }}</p>
      <p>Lingua Originale: {{ item.original_language }}</p>
      <img :src="getImgPath(item.original_language)" alt="">
      <p>Voto: {{ item.vote_average }}</p>
      <p>
        <font-awesome-icon v-for="n in getStarVote(item.vote_average)" :key="n" :icon="['fas', 'star']" />
        <font-awesome-icon v-for="n in 5-getStarVote(item.vote_average)" :key="n" :icon="['far', 'star']" />
      </p>
      <img :src="getPosterPath(item.poster_path)" alt="">
    </div>
  </li>
</template>

<style lang="scss scoped">

</style>