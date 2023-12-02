<script>
import axios from 'axios';
import { RouterView } from 'vue-router'
import Pokemon from './components/Pokemon.vue'

  export default {
    name: 'App',
    data() {
     return {
      pokemons: []
    }
  },
    created: function() {
      axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0')
           .then(res => {
            console.log('Lista de pokemons')
            this.pokemons = res.data.results
           })
  },
  components: { 
    Pokemon
  }}

</script>

<template>
  <header>

    <div class="app">
      <div v-for="(poke,index) in pokemons" :key="index"> 
         <Pokemon :name="poke.name" :url="poke.url" :num="index + 1"/>
      </div>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>

</style>
