<template>
  <header class="header">
    <div class="container_img_header">
      <img
        :src="require('./assets/Pokedex.png')"
        alt="imagem pokedex"
        class="img_header"
      />
    </div>
    <h1 class="h1_title">Pokedex</h1>
  </header>

  <section class="section">
    <label for="pokemonInput">
      Quem é esse Pokémon?
      <input type="text" id="pokemonInput" v-model="pokemonID" />
    </label>
    <button class="searchButton" @click="searchPokemon">Pesquisar</button>
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
export default {
  name: "App",
  data() {
    return {
      pokemonData: {},
      pokemonID: "",
    };
  },
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

<style></style>
