<template lang="html">
  <div class="post" v-if="pokemon">
<div class="light-modal" id="pocketmonster" role="dialog" aria-labelledby="light-modal-label" aria-hidden="false">
        <div class="light-modal-content animated zoomInUp">
            <!-- light modal header -->
            <div class="light-modal-header">
                <h3 class="light-modal-heading"><img src="assets/pocketicon.png" style="position: relative; vertical-align: middle;"/>
        Your Pokemon Pocket</h3>
                <a href="#" @click="ResetOpacity(0.5, true, 'block')" class="light-modal-close-icon" aria-label="close">&times;</a>
            </div>
            <!-- light modal body -->
            <div class="light-modal-body">
                        <div v-if="mypokemondetail.length > 0">
          <table>
            <tr>
              <th></th>
              <th>Name</th>
              <th>Original name</th>
            </tr>
            <tr v-for="(value,propertyName) in mypokemondetail">
              <td><img :src="value.img" :title="propertyName" width="60" height="60"/></td>
              <td>{{ value.name }}</td>
              <td>{{ value.ori_name }}</td>
            </tr>
          </table>
        </div>
        <div v-else>
            <h3 style="text-align:center;">Your pocket is empty.</h3>
        </div>
            </div>
            <!-- light modal footer -->
            <div class="light-modal-footer">
                <a href="#" class="light-modal-close-btn"  @click="ResetOpacity(0.5, true, 'block')" aria-label="close">Close</a>
            </div>
        </div>
    </div>

    <!-- <div class="modal" id="pocketmonster">
      <div class="modal-container">
        <h2><img src="assets/pocketicon.png" style="position: relative; vertical-align: middle;"/>
        Your Pokemon Pocket</h2>
        <div v-if="mypokemondetail.length > 0">
          <table>
            <tr>
              <th></th>
              <th>Name</th>
              <th>Original name</th>
            </tr>
            <tr v-for="(value,propertyName) in mypokemondetail">
              <td><img :src="value.img" :title="propertyName" width="60" height="60"/></td>
              <td>{{ value.name }}</td>
              <td>{{ value.ori_name }}</td>
            </tr>
          </table>
        </div>
        <div v-else>
            <h3 style="text-align:center;">Your pocket is empty.</h3>
        </div>
      <a href="#modal-close" class="close" @click="ResetOpacity(0.5, true, 'block')" style="float:right; margin-top: 30%;position: relative;">Close</a>
      </div>
    </div> -->
    
    <div :id="mypokemondetail.length > 0 ? 'pocket-shake' : 'pocket'">
      <a href="#pocketmonster" @click="setToTop">
      <img src="assets/pocket.png" />
      </a>
    </div>
    <h1 class="post__title icon-pokemon">{{ pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1) }}</h1>
    <h4>Click on moving {{ pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1) }} to catch!</h4>
    <p class="post__body">
      <img id="emotion" :src="pokemon.sprites['front_default']" @click="tangkap(pokemon)" width="120" height="120" />
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
   <div class="post" v-else>
<center><img src="assets/pocket.png" class="pocket-bounces" />
<h4>Please wait....</h4></center>
</div>
</template>
<style>
@keyframes shake {
  10%,
  90% {
    transform: translate3d(-1px, 0, 0);
  }

  20%,
  80% {
    transform: translate3d(2px, 0, 0);
  }

  30%,
  50%,
  70% {
    transform: translate3d(-4px, 0, 0);
  }

  40%,
  60% {
    transform: translate3d(4px, 0, 0);
  }
}
a.close {
    background-color: red;
  box-shadow: 0 5px 0 darkred;
  color: white;
  padding: 1em 1.5em;
  position: relative;
  text-decoration: none;
  text-transform: uppercase;
}

a.close:hover {
  background-color: #ce0606;
  cursor: pointer;
}

a.close:active {
  box-shadow: none;
  top: 5px;
}

* {
  box-sizing: border-box;
}
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
}

td,
th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
@font-face {
  font-family: "Pokemon";
  src: url("/assets/Pokemon_Hollow.ttf") format("truetype");
}
h1.icon-pokemon {
  font-family: "Pokemon";
  font-weight: normal;
  font-style: normal;
}
img.flipthis:active {
  -webkit-transform: scaleX(-1);
  transform: scaleX(-1);
}
img {
  vertical-align: middle;
}
img.emotion:hover {
  src: url("/assets/pokeball.png") no-repeat;
}

.light-modal {
  display: none;
  position: fixed;
  background: transparent;
  top: 0;
  bottom: 0;
  left: 0;
  -ms-flex-align: center;
      align-items: center;
  -ms-flex-pack: center;
      justify-content: center;
  right: 0;
  z-index: 9000;
  transition: background 1s;
  font-size: 16px;
  visibility: hidden;
}

.light-modal-content {
  background: #845ec2;
  color: #fff;
  width: 80%;
  border-radius: .2em;
  position: relative;
  max-height: calc(100vh - 150px);
  line-height: 1.4;
  display: -ms-flexbox;
  display: flex;
  -ms-flex-direction: column;
      flex-direction: column;
}

.light-modal-content img {
  max-width: 100%;
  border-radius: .2em;
}

.light-modal-content.large-content {
  width: 50vw;
}

.light-modal-header {
  padding: 20px 20px 20px 20px;
  background: rgba(0, 0, 0, 0.2);
  display: -ms-flexbox;
  display: flex;
  -ms-flex-pack: justify;
      justify-content: space-between;
  -ms-flex-align: center;
      align-items: center;
}

.light-modal-heading {
  margin: 0;
  font-size: 1.5em;
}

.light-modal-heading + .light-modal-close-icon {
  position: static;
}

.light-modal-body {
  padding: 20px;
  overflow: auto;
  max-height: 450px;
}

.light-modal-footer {
  padding: 20px 20px 20px 20px;
  background: rgba(0, 0, 0, 0.2);
  text-align: right;
  display: -ms-flexbox;
  display: flex;
  -ms-flex-align: center;
      align-items: center;
}

.light-modal-close-icon, .light-modal-close-btn {
  text-decoration: none;
  color: #fff;
  padding: 5px 10px;
  border-radius: .2em;
  background: #FF6F91;
  font-size: 1.5em;
  line-height: 1;
  transition: background .2s ease-in-out;
}

.light-modal-close-icon:hover, .light-modal-close-btn:hover {
  background: #ff3c6a;
}

.light-modal-close-icon {
  position: absolute;
  top: -15px;
  right: -15px;
}

.light-modal-close-btn {
  font-size: 1em;
}

.light-modal-caption {
  position: absolute;
  left: 50%;
  -ms-transform: translateX(-50%);
      transform: translateX(-50%);
  top: 100%;
  padding: 10px 0;
  background: rgba(0, 0, 0, 0.2);
  border-radius: .2em;
  width: 100%;
  text-align: center;
  margin-top: 5px;
}

.light-modal:target {
  background: rgba(0, 0, 0, 0.5);
  display: -ms-flexbox;
  display: flex;
  visibility: visible;
}

.light-modal-navigation .navigation-next,
.light-modal-navigation .navigation-prev {
  width: 32px;
  height: 32px;
  border-color: #fff;
  transition: border-color .2s;
}

.light-modal-navigation .navigation-next:hover,
.light-modal-navigation .navigation-prev:hover {
  border-color: rgba(255, 255, 255, 0.7);
}

.light-modal-navigation .navigation-next {
  position: absolute;
  right: -50px;
  top: 50%;
  border-bottom: 1px solid;
  border-left: 1px solid;
  -ms-transform: rotate(-135deg);
      transform: rotate(-135deg);
}

.light-modal-navigation .navigation-prev {
  position: absolute;
  left: -50px;
  top: 50%;
  border-bottom: 1px solid;
  border-left: 1px solid;
  -ms-transform: rotate(45deg);
      transform: rotate(45deg);
}

@media (max-width: 480px) {
  .light-modal-navigation .navigation-next {
    right: 5px;
  }
  .light-modal-navigation .navigation-prev {
    left: 5px;
  }
}

@keyframes basic {
  0% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

.basic {
  animation-name: basic;
}

@media (max-width: 767px) {
  .light-modal {
    font-size: 14px;
  }
  .light-modal:target .light-modal-content {
    width: 70vw;
  }
}

@supports (display: flex) {
  @media (max-width: 767px) {
    .light-modal:target .light-modal-content {
      width: 70vw;
    }
  }
}
</style>
<script>
import axios from "axios";
export default {
  props: ["name"],
  data() {
    return {
      moveSprites: false,
      mypokemondetail: [],
      pokemon: null,
      speed: 0,
      sprites: [],
      endpoint: "https://pokeapi.co/api/v2/pokemon/"
    };
  },
  watch: {
    $route() {
      this.getPokemon(this.name);
    }
  },
  methods: {
    tangkap(fokemon) {
      this.moveSprites = false;
      let foo = prompt("GOTCHA!! Input your pokemon name:");
      this.mypokemondetail.push({
        img: fokemon.sprites["front_default"],
        ori_name: fokemon.name,
        name: foo
      });
      this.ResetOpacity(0.5, true, "block");
      // (this.mypokemondetail)
    },
    ResetOpacity(val, movesprites, dis) {
      this.moveSprites = movesprites;
      document.getElementsByClassName("column-right")[0].style.opacity = val;
      document.getElementById("emotion").style.display = dis;
    },
    getPokemon(name) {
      // alert('Catch the moving ' + name + ' by click it!')
      // return
      this.pokemon = null;
      axios(this.endpoint + name)
        .then(response => {
          this.speed = 0;
          this.speed = parseInt(response.data.stats[0].base_stat) * 10;
          this.sprites = response.data.sprites;
          this.pokemon = response.data;
          // alert('Catch the moving ' + name + ' by click it!')
        })
        .catch(error => {
          console.log(error);
        });
    },
    setToTop() {
      // alert('tes')
      this.ResetOpacity(1, false, "none");
      setTimeout(function() {
        document.body.scrollTop = 0; // For Safari
        document.documentElement.scrollTop = 0; // For Chrome, Firefox, IE and Opera
      }, 100);
    }
  },

  created() {
    this.getPokemon(this.name);
  },

  mounted() {
    const self = this;
    self.moveSprites = true;
    setTimeout(function() {
      setInterval(function() {
        if (self.moveSprites) {
          var x = Math.floor(Math.random() * self.speed);
          var y = Math.floor(Math.random() * self.speed);
          var obj = document.getElementById("emotion");
          obj.style.position = "absolute";
          obj.style.top = x + "px";
          obj.style.left = y + "px";
        }
      }, self.speed);
    }, 1000);
  }
};
</script>
