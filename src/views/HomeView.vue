<script>
import PokemonList from '../components/PokemonList.vue'

export default {
  data() {
    return {
      filter: ""
    }
  },
  components: {
    PokemonList,
  },
}
</script>

<template>
  <div class="container home">
    <section class="home__random">
      <h2>Liste de pokémons</h2>
      <div class="home__research">
        <p>Ne fonctionne qu'avec les noms anglais</p>
        <input type="text" placeholder="weedle" v-model="filter">
      </div>
      <pokemon-list :filter="filter.toLowerCase()" />
    </section>
  </div>
</template>

<style lang="scss">
@import '@/assets/styles/variables.scss';
@import '@/assets/styles/home.scss';
@import '@/assets/styles/global.scss';
</style>