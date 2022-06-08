<template>
  <div v-if="pokemon" class="pokemon container">
    <img v-if="pokemon.sprites" :src="pokemon.sprites.back_default">
    <div class="pokemon__header">
      <h1 class="capitalize">{{ pokemon.name }}</h1>
      <p><span>{{ pokemon.weight }} kg</span> - <span>{{ pokemon.height }} dm</span></p>
      <div class="pokemon__types">
        <!-- Set un background-color de la bonne couleur en se basant sur notre objet dans data -->
        <div class="pokemon__types__item" v-for="type in pokemon.types" :key="type" :style="'background-color: #' + colorByType[type.type.name]">
          <p class="capitalize">{{ type.type.name }}</p>
        </div>
      </div>
    </div>

    <section>
      <h3>Capacités</h3>
      <div class="pokemon__abilities">
        <div class="pokemon__abilities__item" v-for="ability in pokemon.abilities" :key="ability">
          <p class="capitalize">{{ ability.ability.name }}</p>
        </div>
      </div>
    </section>

    <section>
      <h3>Statistiques</h3>
      <div class="pokemon__stats">
        <div class="pokemon__stats__item" v-for="stat in pokemon.stats" :key="stat">
          <p><span class="capitalize">{{ stat.stat.name }}</span> - <strong>{{ stat.base_stat }}</strong></p>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      pokemon: [],
      // Correspondance de chaque Hexadécimale correspondant à chaque type
      colorByType: {
        'normal' : 'A8A77A',
        'fire': 'EE8130',
        'water': '6390F0',
        'electric': 'F7D02C',
        'grass': '7AC74C',
        'ice': '96D9D6',
        'fighting': 'C22E28',
        'poison': 'A33EA1',
        'ground': 'E2BF65',
        'flying': 'A98FF3',
        'psychic': 'F95587',
        'bug': 'A6B91A',
        'rock': 'B6A136',
        'ghost': '735797',
        'dragon': '6F35FC',
        'dark': '705746',
        'steel': 'B7B7CE',
        'fairy': 'D685AD',
      }
    }
  },
  mounted() {
    // Appelle les infos du dit Pokemon
    let endpoint = new Request('https://pokeapi.co/api/v2/pokemon/' + this.$route.params.name);
    fetch(endpoint)
    .then((response) => response.json())
    .then((data) => {
      this.pokemon = data
    })
  }
}
</script>

<style lang="scss">
.pokemon {
  display: flex;
  flex-direction: column;
  gap: 5rem;

  &__header {
    h1 {
      font-size: 4rem;
    }

    p {
      display: flex;
      width: 100%;
      justify-content: center;
      gap: 1rem;
    }
  }

  &__types {
    display: flex;
    justify-content: center;
    gap: 1rem;
    margin-top: 1rem;

    &__item {
      padding: 0.5rem 1rem;
      border-radius: 5px;

      p {
        font-weight: 600;
        text-transform: uppercase;
        mix-blend-mode: soft-light;
      }
    }
  }

  img {
    width: 100px;
  }

  p {
    font-size: 1.2rem;
  }

  h3 {
    font-size: 2rem;
    margin-bottom: 1rem;
  } 

  &__abilities {
    display: flex;
    gap: 2rem;

    &__item {
      padding: 1rem;
      background-color: #eee;
    }
  }

  &__stats {
    width: 100%;
    max-width: 800px;
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 2rem;

    &__item {
      padding: 1rem;
      background-color: #eee;

      strong {
        font-weight: bolder;
      }
    }
  }
}
</style>