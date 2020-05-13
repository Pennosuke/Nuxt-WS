<template>
  <div class="text-center">
    <h1>POKEDEX</h1>
    <PokeList
      :apiURL="apiURL"
      :imgURL="imgURL"
      @showDetail="showDetail"
    />
    <PokeDetail
      v-if="IsDetailShow"
      :pokeURL="pokeURL"
      :imgURL="imgURL"
    />
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
      this.isDetailShow = true
      console.log('pokeURL = ' + this.pokeURL)
      console.log('IsDetailShow = ' + this.IsDetailShow)
    },
    closeDetail() {
      this.pokeURL = ''
      this.isDetailShow = false
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
