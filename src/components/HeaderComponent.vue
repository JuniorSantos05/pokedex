<template>
  <header class="header">
    <div class="container_img_header">
      <img
        :src="require('../assets/Pokedex.png')"
        alt="imagem pokedex"
        class="img_header"
      />
    </div>
    <h1 class="h1_title">Pokedex</h1>
    <div class="container_text">
      <span>Criado por:</span>
      <h3><a href="https://github.com/JuniorSantos05">Junior Santos</a></h3>
    </div>
  </header>
</template>

<script>
export default {
  name: "HeaderComponent",

  data() {},
};
</script>

<style>
.header {
  width: 100%;
  height: 250px;
  margin: 0;
  padding: 20px;

  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  background-color: #170353;
  color: #f8f8f8;
}

.container_img_header {
  height: 80%;
  display: flex;
  justify-content: center;
}

.img_header {
  margin: 12px;
}

.h1_title {
  display: contents;
  font-size: 50px;
  font-weight: 700;
}

.container_text {
  height: 20px;
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;

  gap: 10px;
  padding: 10px;
}

a {
  color: #f8f8f8;
}
</style>
