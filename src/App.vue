<template>
  <div id="app">
    <header>
      <h1>PokeMan</h1>
    </header>
    <main>

<div class="row">
  <div class="column-left" style="background-color:#aaa;">
 <ul>
    <router-link
        v-for="pokemon in pokemons"
        active-class="is-active"
        class="link"
        :to="{ name: 'PokemonDetail', params: { name: pokemon.name } }">
      <li>{{ pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1) }}</li>
    </router-link>
    </ul>
  </div>
  <div class="column-right" style="background-color:#bbb;">
   <div class="content">
        <router-view></router-view>
      </div>
  </div>
</div>

    </main>
  </div>
</template>
<style>
* {
  box-sizing: border-box;
}

/* Create two equal columns that floats next to each other */
.column {
  float: left;
  width: 20%;
  padding: 10px;
  height: 100%; /* Should be removed. Only for demonstration */
}
.column-left {
  float: left;
  width: 20%;
  padding: 10px;
  height: 50%; /* Should be removed. Only for demonstration */
  overflow: scroll;
}
.column-right {
  float: left;
  width: 80%;
  padding: 10px;
  height: 100%; /* Should be removed. Only for demonstration */
}

.column-sprites {
  float: left;
  width: 25%;
  padding: 10px;
  height: 100%; /* Should be removed. Only for demonstration */
}

/* Clear floats after the columns */
.row:after {
  content: "";
  display: table;
  clear: both;
}
</style>
<script>
import axios from 'axios'
export default {
  data () {
    return {
      pokemons: null,
      endpoint: 'https://pokeapi.co/api/v2/pokemon?offset=0&limit=10000000000000000',
    }
  },

  created() {
    this.getAllPosts();
  },

  methods: {
    getAllPosts() {
      axios.get(this.endpoint)
        .then(response => {
          this.pokemons = response.data.results;
        })
        .catch(error => {
          console.log('-----error-------');
          console.log(error);
        })
    }
  }
}
</script>
