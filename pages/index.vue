<template>
  <div class="list">
    <h1>POKEDEX</h1>
    <ul v-for="(pokemon, index) in pokemons" :key="index">
      <button type="button" class="btn btn-info pokebutton">
        <img :src="imgURL + pokeID[index] + '.png'" class="pokemon-size" />
        <h4>{{ pokemon.name }}</h4>
      </button>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      imgURL: 'https://pokeres.bastionbot.org/images/pokemon/',
      CurrentURL: 'https://pokeapi.co/api/v2/pokemon/?offset=0&limit=20',
      NextURL: '',
      pokemons: [],
      pokeID: []
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      console.log(this.CurrentURL)
      fetch(this.CurrentURL)
        .then((response) => {
          return response.json()
        })
        .then((data) => {
          this.nextUrl = data.next
          data.results.forEach((pokemon) => {
            this.pokeID.push(pokemon.url.split('/').filter(function(part) { return !!part }).pop())
            this.pokemons.push(pokemon)
          })
          console.log(this.pokemon)
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
}
</style>
