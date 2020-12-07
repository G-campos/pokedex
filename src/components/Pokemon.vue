<template>
  <div id="pokemon">
    <div class="card" :class="tipo">
      <div class="card-image">
        <figure>
          <img :src="this.currentImg" alt="Placeholder image" />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{ num }} - {{ name | upper }}</p>
            <p class="subtitle is-6">{{ pokemon.type }}</p>
          </div>
        </div>

        <div class="content">
          <button class="button is-medium is-fullwidth" @click="mudarSprite">Mudar sprite</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  props: {
    num: Number,
    name: String,
    url: String,
    tipo: String,
  },
  data() {
    return {
      isFront: true,
      currentImg: "",
      pokemon: {
        id: "",
        type: "",
        front: "",
        back: "",
      },
    };
  },
  created: function () {
    axios.get(this.url).then((res) => {
      this.pokemon.id = res.data.id;
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      this.currentImg = this.pokemon.front;
    });
  },
  methods: {
    mudarSprite: function () {
      if (this.isFront) {
        this.isFront = false;
        this.currentImg = this.pokemon.back;
      } else {
        this.isFront = true;
        this.currentImg = this.pokemon.front;
      }
    },
  },
  filters: {
    upper: function (value) {
      var newName = value[0].toUpperCase() + value.slice(1);
      return newName;
    },
  },
};
</script>

<style>
#pokemon {
  margin-top: 2%;
}
.card {
  list-style: none;
  padding: 40px;
  color: #222;
  text-align: center;
  border-radius: 20px;
  position: relative;
}

.card::after {
  content: "";
  display: block;
  width: 50%;
  height: 45%;
  border-radius: 100%;
  background-color: #fff;
  opacity: 0.7;
  position: absolute;
  top: 15%;
  left: 25%;
}

.card:hover {
  animation: bounce 0.5s linear;
}

.card-title {
  text-transform: capitalize;
  margin-bottom: 0px;
  font-size: 32px;
  font-weight: normal;
  position: relative;
  z-index: 2;
}

.card-subtitle {
  margin-top: 5px;
  color: #666;
  font-weight: lighter;
  position: relative;
  z-index: 2;
}

.card-image {
  height: 180px;
  position: relative;
  z-index: 2;
}
</style>
