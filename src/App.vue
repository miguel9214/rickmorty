<template>
  <div id="app">
    <div class="hero is-white is-gradient is-bold">
      <div class="hero-body">
        <h1 class="title">
          <span class="has-text-success">R&M</span>
          <span class="subtitle">Personajes</span>
        </h1>
        <button class="button is-success is-rounded" v-on:click="fecth">
          Consultar
        </button>
      </div>
    </div>
    <br />
    <div class="container">
      <div
        class="columns is-desktop is-mobile is-tablet is-multiline is-centered"
      >
        <Character
          v-for="character of characters"
          v-bind:key="character.id"
          v-bind:character="character"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Character from "./components/Character";
import axios from "axios";

export default {
  components: { Character },
  name: "App",
  data: function () {
    return {
      characters: [],
    };
  },

  created() {
    this.fecth();
  },
  methods: {
    fecth() {
      let result = axios
        .get("https://rickandmortyapi.com/api/character")
        .then((res) => {
          this.characters = res.data.results;
        });
    },
  },
};
</script>

<style></style>
