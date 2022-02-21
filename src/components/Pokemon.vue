<template>
  <div>
    <div class="card mb-2">
      <div class="card-image">
        <figure class="has-text-centered">
          <img :class="{'animate__animated': true, 'animate__flip': isFront, 'animate__flip': !isFront}" :src="currentImg" :alt="pokemon.name">
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{ num }} - {{ capitalize(name) }}</p>
            <p class="subtitle is-6">{{ pokemon.type }}</p>
          </div>
        </div>
        <div class="content">          
          <button class="button is-primary" @click="changeSprite()">Virar Pokemon</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'Pokemon',
  props: {
    name: String,
    num: Number,
    url: String,
  },
  data() {
    return {
      isFront: true,
      currentImg: '',
      pokemon: {
        type: '',
        front: '',
        back: '',
      },
    }
  },
  computed: {
    capitalize () {
      return value => value[0].toUpperCase() + value.slice(1);
    }
  },
  methods: {
    changeSprite () {
      if (this.isFront) {
        this.isFront = false;
        this.currentImg = this.pokemon.back;
      } else {
        this.isFront = true;
        this.currentImg = this.pokemon.front;
      }
    }
  },
  created: function() {
    axios.get(this.url)
      .then(res => {
        this.pokemon.type = res.data.types[0].type.name;
        this.pokemon.front = res.data.sprites.front_default;
        this.pokemon.back = res.data.sprites.back_default;
        this.currentImg = this.pokemon.front;
      })
  },
}
</script>

<style>

</style>