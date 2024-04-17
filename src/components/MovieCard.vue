
<script>
  export default {
    props: {
      item: {
        type: Object,
        required: true
      }
    }
  }
</script>

<template>
  <li class="card">
    <div class="card-body">
      <p>Titolo: {{ item.title }}</p>
      <p>Titolo originale: {{ item.original_title }}</p>
      <p>Lingua Originale:{{ item.original_language }}</p>
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