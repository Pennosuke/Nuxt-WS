<template>
  <div class="container list">
    <div v-for="(pokemon, index) in pokemons" :key="index">
      <button type="button" class="btn btn-info pokebutton" @click="showDetail(pokemon.url)">
        <img :src="imgURL + pokeID[index] + '.png'" class="pokemon-size" />
        <h4>{{ pokemon.name }}</h4>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    apiURL: String,
    imgURL: String
  },
  data: () => {
    return {
      pokeID: [],
      pokemons: []
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    async fetchData() {
      const response = await fetch(this.apiURL)
      const data = await response.json()
      data.results.forEach((pokemon) => {
        this.pokeID.push(pokemon.url.split('/').filter(function(part) { return !!part }).pop())
        this.pokemons.push(pokemon)
      })
    },
    showDetail(url) {
      this.$emit('showDetail', url)
    }
  }
}
</script>

<style scoped>
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
