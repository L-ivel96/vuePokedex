<template>
  <div id="app">
    <div class="column is-10 is-offset-1">
      <img src="./assets/logo.png">
      <hr>
      <h4 class="is-size-4">Pokedex</h4>
      <input id="campoBuscar" class="input is-rounded" type="text" placeholder="Buscar" v-model="busca">

      <div class="is-flex is-flex-wrap-wrap is-justify-content-space-evenly">
        <div class="" v-for="poke, index in buscarNaLista" :key="poke.url">
          <Pokemon :num="index+1" :name="poke.name" :url="poke.url"  />
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios';
import Pokemon from './components/Pokemon';

export default {
  name: 'App',
  data() {
    return {
      pokemons: [],
      busca: ''
    }
  },
  created: function() {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      console.log("Salvou pokemons");
      this.pokemons = res.data.results;
    });
  },
  components: {
    Pokemon
  },
  computed: {
    buscarNaLista: function() {
      if(this.busca == '' || this.busca == ' ') {
        return this.pokemons;
      }
      else {
        return this.pokemons.filter(pokemon => pokemon.name.indexOf(this.busca.toLowerCase()) != -1);
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#campoBuscar {
  margin-bottom: 2%;
}
</style>
