<template>
  <div class="text-center">
    <h1>POKEDEX</h1>
    <PokeList :pokemons="pokemons" :pokeID="pokeID"/>
    <!-- <div class="container list">
      <div v-for="(pokemon, index) in pokemons" :key="index">
        <button type="button" class="btn btn-info pokebutton">
          <img :src="imgURL + pokeID[index] + '.png'" class="pokemon-size" />
          <h4>{{ pokemon.name }}</h4>
        </button>
      </div>
    </div> -->
  </div>
</template>

<script>
import PokeList from '~/components/PokeList.vue'
export default {
  components: {
    PokeList
  },
  data() {
    return {
      apiURL: 'https://pokeapi.co/api/v2/pokemon/?offset=0&limit=20',
      pokemons: [],
      pokeID: [],
      pokeURL: '',
      showDetail: false
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      fetch(this.apiURL)
        .then((response) => {
          return response.json()
        })
        .then((data) => {
          data.results.forEach((pokemon) => {
            this.pokeID.push(pokemon.url.split('/').filter(function(part) { return !!part }).pop())
            this.pokemons.push(pokemon)
          })
        })
        .catch((error) => {
          console.log(error)
        })
    }
  }
}
</script>

<style>
.pokemon-size {
  width: 95px;
  height: 95px;
}
.pokebutton {
  width: 200px;
  height: 200px;
  border-radius: 20px;
  box-shadow: -1.2px 13.9px 32px 0 rgba(60, 60, 62, 0.27);
  margin-top: 20px;
  margin-bottom: 20px;
}
.list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  grid-gap: 10px;
  width: 100%;
  max-width: 800px;
}
</style>
