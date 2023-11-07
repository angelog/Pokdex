<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <div v-for="(poke, index) in pokemons" :key="index">
        <Pokemon :name="poke.name" :url="poke.url" :num="index +1" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from './components/Pokemon.vue'
export default {
  name: 'App',
  components: {
    Pokemon
  },
  data() {
    return {
      pokemons: []
    }
  },
  created: function() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0')
    
      .then((res) => {
        this.pokemons = res.data.results;
      })
    
      .catch(error => console.log(error));
    console.log(this.pokemons);
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  background-color: rgba(0, 0, 0, 0.61);
}

</style>
