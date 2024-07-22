<script>
import axios from 'axios'
import InfoModal from './InfoModal.vue';
import { store } from '../store';

  export default {
    props: {
      item: {
        type: Object,
        required: true
      }
    },
    components: {
      InfoModal
    },
    data(){
      return {
          isModalVisible: false,
          gotInfo: false,
          store: store,
          info: {},
          flags: [
              {
                  language: 'en',
                  flag: '/flags/english.png'
              },
              {
                  language: 'it',
                  flag: '/flags/italian.png'
              },
              {
                  language: 'fr',
                  flag: '/flags/french.png'
              },
              {
                  language: 'es',
                  flag: '/flags/spanish.png'
              },
          ]
      }
    },
    methods: {
      fetchInfo(){
            if (this.gotInfo == false){
              axios.get(`https://api.themoviedb.org/3/tv/${this.item.id}?api_key=952819b1623493b0abb662f846bd0331`).then((res) => {
              store.currentInfo = res.data
              })
              this.gotInfo = true
              console.log(store.currentInfo)
            }
        },
      showModal() {
      this.isModalVisible = true;
      document.body.classList.add('modal-open')
      },
      closeModal() {
        this.isModalVisible = false;
      document.body.classList.remove('modal-open')
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
        if (this.item.name == this.item.original_name) {
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
    <img v-else class="poster h-100 w-100 z-2 p-4" src="https://ouch-cdn2.icons8.com/oUSOvdU3-qOpsDEsyA3XdoROq4gPnbYncCh9XbUhse4/rs:fit:368:670/czM6Ly9pY29uczgu/b3VjaC1wcm9kLmFz/c2V0cy9zdmcvNDI5/L2ZlOGJhYjAyLTZi/OWEtNDJkYy1iZjA0/LTA2M2FhODBiYjMw/Mi5zdmc.png" alt="">
    <div class="info h-100 w-100 p-3 z-3">
      <p class="card-title fw-bold fs-5">{{ item.name }}</p>
      <p>First Episode: {{ item.first_air_date }}</p>
      <p v-if="areNamesEquals == false">Original Title: {{ item.original_name }}</p>
      <p>Original Language: {{ item.original_language }}</p>
      <p>Vote: {{ getVote() }}</p>
      <p>
        <font-awesome-icon v-for="n in getStarVote(item.vote_average)" :key="n" :icon="['fas', 'star']" />
        <font-awesome-icon v-for="n in 5-getStarVote(item.vote_average)" :key="n" :icon="['far', 'star']" />
      </p>
      <button class="btn btn-outline-secondary" @click="fetchInfo(); showModal()"> INFO </button>
      <img class="lang" :src="getImgPath(item.original_language)" alt="">
      <Teleport to="body">
        <InfoModal v-show="isModalVisible" @close="closeModal" :item="this.item" :info="store.currentInfo"/>
      </Teleport>
    </div>
  </div>
</template>

<style lang="scss scoped">

</style>