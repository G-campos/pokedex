<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter container">
      <img src="./assets/pokedex.png" />
      <hr />
      <input class="input is-rounded" type="text" placeholder="Buscar pokemon pelo nome" v-model="busca" />
      <button class="button is-fullwidth is-success" id="buscaBtn" @click="buscar">Buscar</button>
      <!--<div v-for="(poke, index) in resultadoBusca" :key="index">-->
      <div v-for="(poke, index) in filteredPokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" :tipo="poke.type" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";
export default {
  name: "App",
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: "",
    };
  },
  created: function () {
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then((res) => {
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    });
  },
  components: {
    Pokemon,
  },
  computed: {
    // resultadoBusca: function () {
    //   if (this.busca == "" || this.busca == " ") {
    //     return this.pokemons;
    //   } else {
    //     return this.pokemons.filter((pokemon) => pokemon.name == this.busca);
    //   }
    // },
  },
  methods: {
    buscar: function () {
      this, (this.filteredPokemons = this.pokemons);
      if (this.busca == "" || this.busca == " ") {
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter((pokemon) => pokemon.name == this.busca);
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: #efefbb;
  background: linear-gradient(to right, rgb(197, 230, 236), rgb(239, 187, 230));
  color: white;
  margin: 0;
  font-family: rubik;
}

#buscaBtn {
  margin-top: 2%;
}

.container {
  padding: 40px;
  margin: 0 auto;
}

h1 {
  text-align: center;
  font-size: 54px;
}

.pokedex {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
  grid-gap: 20px;
  padding-inline-start: 0;
}

.steel {
  background-color: #f4f4f4;
}

.fire {
  background-color: #fddfdf;
}

.grass {
  background-color: #defde0;
}

.electric {
  background-color: #fcf7de;
}

.water,
.ice {
  background-color: #def3fd;
}

.ground {
  background-color: #f4e7da;
}

.rock {
  background-color: #d5d5d4;
}

.fairy {
  background-color: #fceaff;
}

.poison {
  background-color: #98d7a5;
}

.bug {
  background-color: #f8d5a3;
}

.dragon {
  background-color: #97b3e6;
}

.psychic {
  background-color: #eaeda1;
}

.flying {
  background-color: #f5f5f5;
}

.fighting {
  background-color: #e6e0d4;
}

.normal {
  background-color: #f5f5f5;
}

@keyframes bounce {
  20% {
    transform: translateY(-6px);
  }
  40% {
    transform: translateY(0px);
  }

  80% {
    transform: translateY(-2px);
  }
  100% {
    transform: translateY(0);
  }
}
</style>
