<template>
  <router-link class="pokemon-card" v-if="pokemon" :to='"/pokemon/" + pokemon.id'>
    <p class="capitalize">{{ data.name }}</p>
    <img :src="pokemon.sprites.back_default">
  </router-link>
</template>

<script>
export default {
  props: ['data'],
  data() {
    return {
      pokemon: undefined
    }
  },
  mounted() {
    let endpoint = new Request(this.data.url);
    fetch(endpoint)
    .then((response) => response.json())
    .then((data) => {
      this.pokemon = data
    })
  }
}
</script>

<style lang="scss">
.pokemon-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: #eee;
  padding: 2rem 1rem;
  border-radius: 5px;
  cursor: pointer;
  color: black;
  text-decoration: none;
} 
</style>