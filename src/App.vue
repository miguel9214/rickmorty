<template>
  <div id="app">
    <h1 class="title">Consultar datos</h1>
  </div>
  <button v-on:click="fecth">Consultar</button>
  <div v-for="personaje of personajes" v-bind:key="personaje.id">
    {{ personaje.id }}
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data: function () {
    return {
      personajes: [],
    };
  },
  methods: {
    fecth() {
      let result = axios
        .get("https://rickandmortyapi.com/api/character")
        .then((res) => {
          this.personajes = res.data.results;
        });
    },
  },
};
</script>

<style></style>
