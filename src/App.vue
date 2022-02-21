<template>
  <div class="app" id="app">
    <Navbar :title="title" @getQuery="returnQuery($event)" />
    <div class="column is-half is-offset-one-quarter">
      <div v-for="(poke, i) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :num="i + 1" :url="poke.url" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

import Navbar from "./components/Navbar.vue";
import Pokemon from "./components/Pokemon.vue";

export default {
  name: "App",
  components: {
    Navbar,
    Pokemon,
  },
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      title: process.env.VUE_APP_TITLE,
    }
  },
  computed: {
    
  },
  methods: {
    returnQuery($event) {
      this.filteredPokemons = this.pokemons;

      if ($event === undefined || $event === '' || $event === ' ') { 
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name === $event);
      }
    }
  },
  created: function() {
    axios.get(process.env.VUE_APP_API_URL)
      .then(res => {
        this.pokemons = res.data.results;
        this.filteredPokemons = res.data.results;
      })
      .catch(error => console.error(error));    
  },
};
</script>

<style>
</style>