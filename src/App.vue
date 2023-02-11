<template>
  <HeaderComponent />

  <section class="section">
    <div class="searchContainer">
      <h2 class="searchTitle">Digite o ID ou nome do Pokemon</h2>
      <div class="inputContainer">
        <label for="pokemonInput">
          <input
            class="searchInput"
            type="text"
            id="pokemonInput"
            v-model="pokemonID"
            @keyup.enter="searchPokemon"
          />
        </label>
        <button class="searchButton" @click="searchPokemon">Pesquisar</button>
      </div>
    </div>
  </section>

  <main class="main" v-if="Object.entries(pokemonData).length > 0">
    <section class="pokemonCard">
      <div class="nameImage">
        <h1 class="pokemonName">
          {{
            pokemonData.name.charAt(0).toUpperCase() + pokemonData.name.slice(1)
          }}
        </h1>

        <div class="boxImg">
          <img
            :src="pokemonData.sprites.front_default"
            :alt="pokemonData.name"
          />
        </div>
        <button class="toogleBtn" @click="showDetails = !showDetails">+</button>
      </div>
      <div class="pokemonTypes">
        <ul class="type" v-if="showDetails">
          <h2>Type:</h2>
          <li
            v-for="(type, key) in pokemonData.types"
            :key="key"
            :class="type.type.name"
          >
            <span>{{ type.type.name }}</span>
          </li>
        </ul>
        <ul class="stats" v-if="showDetails">
          <h2>Stats:</h2>
          <li v-for="(stat, key) in pokemonData.stats" :key="key">
            <span>{{ stat.stat.name }} => {{ stat.base_stat }}</span>
          </li>
        </ul>
      </div>
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
      showDetails: false,
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

#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.searchTitle {
  margin: 50px 0 8px 0;
  font-size: 22px;
  font-weight: 700;
}

@media only screen and (min-width: 768px) and (max-width: 959px) {
  .searchTitle {
    font-size: 20px;
  }
}

@media only screen and (min-width: 480px) and (max-width: 767px) {
  .searchTitle {
    font-size: 17px;
  }
}

@media only screen and (max-width: 479px) {
  .searchTitle {
    font-size: 16px;
  }
}

.searchInput {
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

.searchContainer {
  display: flex;
  flex-direction: column;
  max-width: 100%;
  align-items: center;
}

.inputContainer {
  display: flex;
  gap: 10px;
}

.pokemonCard {
  display: flex;
  justify-content: center;
  align-content: center;
  flex-direction: row;
  align-items: center;
  margin-top: 30px;
  gap: 40px;
}

@media only screen and (max-width: 767px) {
  .pokemonCard {
    flex-direction: column;
  }
}

.boxImg {
  background-color: #170353;
  border-radius: 50%;
  display: flex;
  width: 200px;
  height: 200px;
  justify-content: center;
  align-items: center;
}

.boxImg img {
  width: 100%;
}

.nameImage {
  display: flex;
  position: relative;
  flex-direction: row-reverse;
  align-items: center;
  justify-content: space-evenly;
  padding: 10px;
  gap: 20px;
  border-radius: 6px;
  box-shadow: 1px 1px #170353, 2px 2px #170353, 3px 3px #170353;
  transition: 0.3s;
}

.toogleBtn {
  position: absolute;
  right: 10px;
  bottom: 10px;
  cursor: pointer;
  border-radius: 4px;

  font-size: 20px;
  font-weight: 400;

  background-color: #170353;
  color: #f8f8f8;
  transition: 0.3s;
}

.toogleBtn:hover {
  background-color: #512dbc;
}

.pokemonTypes {
  width: 35%;
  min-width: 360px;
  max-width: 400px;
  display: flex;
  flex-direction: row;
  align-items: flex-start;
  gap: 30px;
  box-shadow: 1px 1px #170353, 2px 2px #170353, 3px 3px #170353;
}

.pokemonTypes ul {
  list-style: none;
}
</style>
