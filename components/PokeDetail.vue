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
        <div v-for="(value, index) in pokemon.types" :key="index" :data-color="value.type.name" class="type">
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
.type[data-color = "bug"] {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #6D7815;
}
.type[data-color = "dark"] {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #49392F;
}
.type[data-color = "dragon"] {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #4924A1;
}
.type[data-color = "electric"] {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #A1871F;
}
.type[data-color = "fairy"] {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #9B6470;
}
.type[data-color = "fighting"] {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #7D1F1A;
}
.type[data-color = "fire"] {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #9C531F;
}
.type[data-color = "flying"] {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #6D5E9C;
}
.type[data-color = "ghost"] {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #493963;
}
.type[data-color = "grass"] {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #4E8234;
}
.type[data-color = "ground"] {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #927D44;
}
.type[data-color = "ice"] {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #638D8D;
}
.type[data-color = "normal"] {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #6D6D4E;
}
.type[data-color = "poison"] {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #682A68;
}
.type[data-color = "psychic"] {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #A13959;
}
.type[data-color = "rock"] {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #786824;
}
.type[data-color = "steel"] {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
  background-color: #787887;
}
.type[data-color = "water"] {
  margin-bottom: 10px;
  margin-inline: 5px;
  padding-top: 5px;
  padding-inline: 10px;
  border-radius: 30px;
  color: #ffffff;
  letter-spacing: 2px;
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
