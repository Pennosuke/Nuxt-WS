<template>
  <div>
    <ul v-for="(pokemon, index) in pokemons" :key="index">
      <li>
        <!-- <img src="imageURL + pokeID[index] + '.png'" class="pokemon-size" /> -->
        <h3>{{ pokemon.name }}</h3>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    imageURL: {
      type: String,
      default: ''
    },
    apiURL: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      CurrentURL: '',
      NextURL: '',
      pokemons: [],
      pokeID: []
    }
  },
  mounted() {
    this.CurrentURL = this.apiURL
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
          /* this.nextUrl = data.next */
          data.results.forEach((pokemon) => {
            /* pokemon.id = pokemon.url.split('/').filter(function(part) { return !!part }).pop() */
            this.pokemons.push(pokemon)
          })
          console.log(this.pokemon)
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
</style>
