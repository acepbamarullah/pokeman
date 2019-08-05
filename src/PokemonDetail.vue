<template lang="html">
  <div class="post" v-if="pokemon">
    <h1 class="post__title icon-pokemon"><img id="emotion" :src="pokemon.sprites['front_default']" @click="tangkap(pokemon)"/> {{ pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1) }}</h1>
    <p class="post__body">
      Another form (click to flip):
      <div class="row">
  <div class="column-sprites" v-if="value" v-for="(value,propertyName) in pokemon.sprites">
  <img class="flipthis" :src="value" :title="propertyName" />
</div>
</div>
Height: {{ pokemon.height }}<br>
Weight: {{ pokemon.weight }}<br>
Abilities:
      <ul id="abilities">
        <li v-for="pok in pokemon.abilities">
          {{ pok.ability.name }}
        </li>
      </ul>
Types:
      <ul id="types">
        <li v-for="type in pokemon.types">
          {{ type.type.name }}
        </li>
      </ul>
Statistic:
      <ul id="stats">
        <li v-for="st in pokemon.stats">
          {{ st.stat.name }}: {{ st.base_stat }}
        </li>
      </ul>
Moves:
      <ul id="moves">
        <li v-for="mv in pokemon.moves">
          {{ mv.move.name }}
        </li>
      </ul>
    </p>
    <p class="post__id"></p>
  </div>
</template>
<style>
@font-face {
font-family: "Pokemon";
src: url("/assets/Pokemon_Hollow.ttf") format("truetype");
}
h1.icon-pokemon {
  font-family: 'Pokemon';
  font-weight:normal;
  font-style:normal;
}
img.flipthis:active {
  -webkit-transform: scaleX(-1);
  transform: scaleX(-1);
}
img {
  vertical-align: middle;
}
img.emotion:hover {
  src: url('/assets/pokeball.png') no-repeat;
}
</style>
<script>
import axios from 'axios';
export default {
  props: ['name'],
  data() {
    return {
      pokemon: null,
      speed: 0,
      sprites: [],
      endpoint: 'https://pokeapi.co/api/v2/pokemon/',
    }
  },
  watch: {
  '$route'() {
    this.getPokemon(this.name);
  }
},
  methods: {
    tangkap(fokemon) {
    // alert('tes');
    console.log(fokemon);
    },
  getPokemon(name) {
    axios(this.endpoint + name)
      .then(response => {
        this.pokemon = null
        this.speed  = parseInt(response.data.stats[0].base_stat) * 10
        this.sprites  = response.data.sprites
        this.pokemon = response.data
      })
      .catch( error => {
        console.log(error)
      })
  }
},

created() {
  this.getPokemon(this.name);
},

mounted() {
      const self = this
 setTimeout(function(){
 setInterval(function(){
  var x = Math.floor(Math.random() * self.speed);
var y = Math.floor(Math.random() * self.speed);
var obj = document.getElementById("emotion");
obj.style.position = 'absolute';
obj.style.top = x + "px";
obj.style.left = y + "px";
 }, self.speed);
  }, 1000);
}
}
</script>
