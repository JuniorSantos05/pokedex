<template>
  <HeaderComponent />

  <section class="section">
    <div class="search_container">
      <h2 class="input_title">Quem é esse Pokémon?</h2>
      <div class="input_container">
        <label for="pokemonInput">
          <input type="text" id="pokemonInput" v-model="pokemonID" />
        </label>
        <button class="searchButton" @click="searchPokemon">Pesquisar</button>
      </div>
    </div>
  </section>

  <main class="main" v-if="Object.entries(pokemonData).length > 0">
    <section class="pokemonCard">
      <div class="nameImage">
        <h1 class="pokemonName">{{ pokemonData.name }}</h1>
        <img :src="pokemonData.sprites.front_default" :alt="pokemonData.name" />
      </div>
      <ul class="type">
        <h2>Type:</h2>
        <li
          v-for="(type, key) in pokemonData.types"
          :key="key"
          :class="type.type.name"
        >
          <span>{{ type.type.name }}</span>
        </li>
      </ul>
      <ul class="stats">
        <h2>Stats:</h2>
        <li v-for="(stat, key) in pokemonData.stats" :key="key">
          <span>{{ stat.stat.name }} => {{ stat.base_stat }}</span>
        </li>
      </ul>
    </section>
  </main>
</template>

<script>
import { baseUrl } from "./Api";
import HeaderComponent from "./components/HeaderComponent.vue";
export default {
  name: "App",
  data() {
    return {
      pokemonData: {},
      pokemonID: "",
    };
  },
  components: { HeaderComponent },
  methods: {
    async searchPokemon() {
      try {
        const whoIsThisPokemon = await fetch(`${baseUrl}/${this.pokemonID}`);
        const pokemon = await whoIsThisPokemon.json();
        this.pokemonData = pokemon;
        console.log(pokemon);
        return pokemon;
      } catch (error) {
        alert("Pokemon was not found");
      }
    },
  },
};
</script>

<style>
body {
  font-family: "Varela Round", sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.input_title {
  margin: 50px 0 8px 0;
  font-size: 2rem;
  font-weight: 700;
}

input {
  padding: 8px 0 8px;
  max-width: 100%;
  min-width: 0;
  width: 50vw;

  border-radius: 5px;
}

.searchButton {
  width: 100px;
  border-radius: 5px;
  font-weight: 400;
  color: #f8f8f8;
  background-color: #170353;
  cursor: pointer;
  transition: 0.3s;
}

.searchButton:hover {
  background-color: #512dbc;
}

.search_container {
  display: flex;
  flex-direction: column;
  max-width: 100%;
  align-items: center;
}

.input_container {
  display: flex;
  gap: 10px;
}
</style>
