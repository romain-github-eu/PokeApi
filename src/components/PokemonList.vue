<template>
  <div class="pokemon-list">
    <!-- Pour chaque pokemon, rend un PokemonCard en passant pokemon dans la props data -->
    <pokemon-card v-for="(pokemon) in filtered" :key="pokemon.name" :data="pokemon"/>
  </div>
</template>

<script>
import PokemonCard from './PokemonCard.vue'
export default {
  props: ['filter'],
  components: {
    PokemonCard
  },
  data() {
    return {
      pokemons: [],
      filtered: []
    }
  },
  mounted() {
    this.getPokemons()
  },
  watch: {
    // Filter les pokemons a chaque changement et bloque le nombre max de résultat à 25 (pour ne pas surcharger le DOM)
    filter() {
      this.filtered = this.pokemons.filter(el => el.name.includes(this.filter)).slice(0, 25)
    }
  },
  methods: {
    getPokemons() {
      // A l'init du composant, appelle tous les pokemons
      let endpoint = new Request('https://pokeapi.co/api/v2/pokemon?limit=10000');
      fetch(endpoint)
      .then((response) => response.json())
      .then(({ results }) => {
        this.pokemons = results
        this.filtered = results.slice(0, 25)
      })
    }
  }
}
</script>

<style lang="scss">
.pokemon-list {
  width: 100%;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 2rem;
}
</style>