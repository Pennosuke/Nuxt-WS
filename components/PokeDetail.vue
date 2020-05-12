<template>
  <div class="detail">
    <div v-if="show" class="detail-view">
      <div v-if="pokemon" class="image">
        <img :src="imgURL + pokeID[index] + '.png'" class="pokemon-size" />
      </div>
      <div v-if="pokemon" class="data">
        <h2>
          {{pokemon.name}}
        </h2>
        <div class="property">
          <div class="left">
            Base Experience
          </div>
          <div class="right">
            {{ pokemon.base_experience }}
          </div>
        </div>
      </div>
    </div>
    <i v-else class="fas fa-spinner fa-spin"></i>
  </div>
</template>

<script>
export default {
  props: {
    pokeURL: String
  },
  data: () => {
    return {
      imgURL: 'https://pokeres.bastionbot.org/images/pokemon/',
      show: false,
      pokemon: {}
    }
  },
  created() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      fetch(this.pokeURL)
        .then((response) => {
          return response.json()
        })
        .then((data) => {
          this.pokemon = data
        })
        .catch((error) => {
          console.log(error)
        })
    }
  }
}
</script>

<style scoped>
.detail {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  position: fixed;
  top: 0;
  left: 0;
  padding: 90px 10px 10px;
  width: calc(100% - 20px);
  height: calc(100vh - 20px);
}
.detail-view {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  position: relative;
  width: 100%;
  max-width: 510px;
  padding: 50px 0 0;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 15px 30px rgba(0,0,0,.2),
              0 10px 10px rgba(0,0,0,.2);
}
.image {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  top: -60px;
  width: 120px;
  height: 120px;
  background-color: #333;
  border-radius: 50%;
  overflow: hidden;
  box-shadow: 0 15px 30px rgba(0,0,0,.2),
              0 10px 10px rgba(0,0,0,.2);
}
.pokemon-size {
  width: 95px;
  height: 95px;
}
.data {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  flex-direction: column;
  width: 100%;
  margin-bottom: 40px;
}
</style>
