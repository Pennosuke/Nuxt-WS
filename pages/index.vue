<template>
  <div class="text-center">
    <h1>POKEDEX</h1>
    <poke-list v-if="!IsDetailShow" :apiURL="apiURL" :imgURL="imgURL" @showDetail="showDetail"></poke-list>
    <poke-detail v-if="IsDetailShow" :pokeURL="pokeURL" :imgURL="imgURL" @closeDetail="closeDetail"></poke-detail>
  </div>
</template>

<script>
import PokeList from '~/components/PokeList.vue'
import PokeDetail from '~/components/PokeDetail.vue'
export default {
  components: {
    PokeList,
    PokeDetail
  },
  data: () => {
    return {
      apiURL: 'https://pokeapi.co/api/v2/pokemon/?offset=0&limit=20',
      imgURL: 'https://pokeres.bastionbot.org/images/pokemon/',
      pokeURL: '',
      IsDetailShow: false
    }
  },
  methods: {
    showDetail(url) {
      this.pokeURL = url
      this.IsDetailShow = true
    },
    closeDetail() {
      this.pokeURL = ''
      this.IsDetailShow = false
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
  box-shadow: -1.2px 13.9px 32px rgba(60, 60, 62, 0.27);
  margin-top: 20px;
  margin-bottom: 20px;
}
</style>
