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
            // let lang =  this.flags.find((country) => country.language == abbreviation)
            // console.log(lang)
            // return lang
            let lang =this.flags.find((country) => country.language == abbreviation)
            if (lang !== undefined) {
                console.log(abbreviation)
                console.log(lang.flag)
                return lang.flag
            }
        },
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
        <font-awesome-icon v-for="n in 5" :key="n" :icon="['fas', 'star']" />
        <font-awesome-icon :icon="['far', 'star']" />
      </p>
    </div>
  </li>
</template>

<style lang="scss scoped">

</style>