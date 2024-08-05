<script>
 export default {
  props: {
      item: {
        type: Object,
        required: true
      },
      info: {
        type: Object,
        required: true
      },
    },
    name: 'Modal',
    methods: {
      close() {
        this.$emit('close');
      },
      getPosterPath(path) {
        console.log()
        return `https://image.tmdb.org/t/p/w342${path}`
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
  };
</script>

<template>
        <div class="modal-backdrop">
            <div class="infoModal">
                <img v-if="item.poster_path != null" class="poster h-100 " :src="getPosterPath(item.poster_path)" alt="">
                <img v-else class="poster h-100 z-2 p-4" src="https://ouch-cdn2.icons8.com/oUSOvdU3-qOpsDEsyA3XdoROq4gPnbYncCh9XbUhse4/rs:fit:368:670/czM6Ly9pY29uczgu/b3VjaC1wcm9kLmFz/c2V0cy9zdmcvNDI5/L2ZlOGJhYjAyLTZi/OWEtNDJkYy1iZjA0/LTA2M2FhODBiYjMw/Mi5zdmc.png" alt="">
                <div class="info h-100 w-50 d-flex flex-column p-4">
                  <p class="fs-5">{{ item.title }}</p>
                  <p v-if="areNamesEquals == false">Original Title: {{ item.original_title }}</p>
                  <p>Original Language: {{ item.original_language }}</p>
                  <p>Vote: {{ getVote() }}</p>
                  <p>
                    <font-awesome-icon v-for="n in getStarVote(item.vote_average)" :key="n" :icon="['fas', 'star']" />
                    <font-awesome-icon v-for="n in 5-getStarVote(item.vote_average)" :key="n" :icon="['far', 'star']" />
                  </p>
                  <p>{{ info.overview }}</p>
                  <p><a :href="info.homepage">Official Website</a></p>
                  <button type="button" class="close ms-auto mt-auto" @click="close">X</button>
                </div>
            </div>
        </div>
</template>


<style lang="scss">
</style>