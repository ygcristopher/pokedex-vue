<script>
import axios from 'axios';
import { RouterView } from 'vue-router'
import Pokemon from './components/Pokemon.vue'

export default {
  name: 'App',
  data() {
    return {
      pokemons: [],
      filteredPokemons:[],
      search:'',
    }
  },
  created: function () {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0')
      .then(res => {
        console.log('Lista de pokemons')
        this.pokemons = res.data.results
        this.filteredPokemons = res.data.results
      })
  },
  components: {
    Pokemon
  },
  methods: {
    performSearch: function () {
      this.filteredPokemons = this.pokemons;
      if(this.search == '' || this.search == ' '){
        this.filteredPokemons = this.pokemons;
      }else {
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.search)
      }
    }
  },
}

</script>

<template>
  <header>
    <div class="app">
      <div class="column is-half is-offset-one-quarter">
        <input type="text" class="input is-normal" placeholder="Search Pokemon" v-model="search">
        <button class="button is-success" id="search-btn" @click="performSearch">Search</button>
        <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
          <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
        </div>
      </div>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>
  #search-btn {
    margin-top: 1rem;
    width: 100%;
  }
</style>
