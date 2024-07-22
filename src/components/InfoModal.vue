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
          return `https://image.tmdb.org/t/p/w342${path}`
      }
    },
  };
</script>

<template>
        <div class="modal-backdrop">
            <div class="infoModal">
                <img v-if="item.poster_path != null" class="poster h-100 z-2" :src="getPosterPath(item.poster_path)" alt="">
                <img v-else class="poster h-100 z-2 p-4" src="https://ouch-cdn2.icons8.com/oUSOvdU3-qOpsDEsyA3XdoROq4gPnbYncCh9XbUhse4/rs:fit:368:670/czM6Ly9pY29uczgu/b3VjaC1wcm9kLmFz/c2V0cy9zdmcvNDI5/L2ZlOGJhYjAyLTZi/OWEtNDJkYy1iZjA0/LTA2M2FhODBiYjMw/Mi5zdmc.png" alt="">
                <button type="button" class="btn-close" @click="close" >x</button>
                <button type="button" class="btn-green" @click="close">Close Modal</button>
            </div>
        </div>
</template>


<style lang="scss">
</style>