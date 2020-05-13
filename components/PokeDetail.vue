<template>
  <div class="container">
    <img :src="imgURL + pokeID + '.png'" class="pokemon-size" />
    <div class="row">
      <div class="col-md-12">
        <h2>{{ pokemon.name }}</h2>
      </div>
    </div>
    <div class="row bottom-line">
      <div class="col-md-6">
        <h4>Base Experience</h4>
      </div>
      <div class="col-md-6">
        <h4>{{ pokemon.base_experience }}</h4>
      </div>
    </div>
    <div class="row bottom-line">
      <div class="col-md-6">
        <h4>Height</h4>
      </div>
      <div class="col-md-6">
        <h4>{{ pokemon.height }}</h4>
      </div>
    </div>
    <div class="row bottom-line">
      <div class="col-md-6">
        <h4>Weight</h4>
      </div>
      <div class="col-md-6">
        <h4>{{ pokemon.weight }}</h4>
      </div>
    </div>
    <div class="row bottom-line">
      <div class="col-md-6">
        <h4>Type</h4>
      </div>
      <div class="col-md-6 rounded-square-area">
        <div v-for="(value, index) in pokemon.types" :key="index" class="type">
          <h5>{{value.type.name}}</h5>
        </div>
      </div>
    </div>
    <div class="row bottom-line">
      <div class="col-md-6">
        <h4>Abilities</h4>
      </div>
      <div class="col-md-6 rounded-square-area">
        <div v-for="(value, index) in pokemon.abilities" :key="index" class="ability">
          <h5>{{value.ability.name}}</h5>
        </div>
      </div>
    </div>
    <button type="button" class="btn btn-primary" @click="closeDetail">Close</button>
  </div>
</template>

<script>
export default {
  props: {
    pokeURL: String,
    imgURL: String
  },
  data: () => {
    return {
      show: false,
      pokemon: {},
      pokeID: ''
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    async fetchData() {
      const response = await fetch(this.pokeURL)
      const data = await response.json()
      this.pokemon = data
      this.pokeID = this.pokeURL.split('/').filter(function(part) { return !!part }).pop()
    },
    closeDetail() {
      this.$emit('closeDetail')
    }
  }
}
</script>

<style scoped>
.pokemon-size {
  width: 95px;
  height: 95px;
}
.bottom-line {
  border-bottom: 1px solid #cccccc;
  margin-bottom: 10px;
  width: 100%;
}
.rounded-square-area {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
.type {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #0A2E50;
}
.ability {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #A37523;
}
</style>
