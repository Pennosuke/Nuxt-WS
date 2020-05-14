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
        <div v-for="(value, index) in pokemon.types" :key="index" :data-color="value.type.name" class="type type-color">
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
    <div class="row">
      <div class="col-md-12">
        <h2>Stats</h2>
      </div>
    </div>
    <div class="row">
      <div v-for="(value, index) in pokemon.stats" :key="index" class="flex col-md-2 col-xs-1">
        <h5>{{ value.stat.name }}</h5>
        <h4>{{ value.base_stat }}</h4>
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
}
.type-color[data-color = "bug"] {
  background-color: #6D7815;
}
.type-color[data-color = "dark"] {
  background-color: #49392F;
}
.type-color[data-color = "dragon"] {
  background-color: #4924A1;
}
.type-color[data-color = "electric"] {
  background-color: #A1871F;
}
.type-color[data-color = "fairy"] {
  background-color: #9B6470;
}
.type-color[data-color = "fighting"] {
  background-color: #7D1F1A;
}
.type-color[data-color = "fire"] {
  background-color: #9C531F;
}
.type-color[data-color = "flying"] {
  background-color: #6D5E9C;
}
.type-color[data-color = "ghost"] {
  background-color: #493963;
}
.type-color[data-color = "grass"] {
  background-color: #4E8234;
}
.type-color[data-color = "ground"] {
  background-color: #927D44;
}
.type-color[data-color = "ice"] {
  background-color: #638D8D;
}
.type-color[data-color = "normal"] {
  background-color: #6D6D4E;
}
.type-color[data-color = "poison"] {
  background-color: #682A68;
}
.type-color[data-color = "psychic"] {
  background-color: #A13959;
}
.type-color[data-color = "rock"] {
  background-color: #786824;
}
.type-color[data-color = "steel"] {
  background-color: #787887;
}
.type-color[data-color = "water"] {
  background-color: #445E9C;
}
.ability {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #44685E;
}
</style>
