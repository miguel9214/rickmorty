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
      <div class="columns is-desktop is-mobile is-tablet is-multiline is-centered">
        <Character v-for="character of characters" v-bind:key="character.id" v-bind:character="character" />
      </div>
      <nav class="pagination" role="navigation" aria-label="pagination">
        <a class="pagination-previous" v-on:click="changedPage(page - 1)">Anterior</a>
        <ul class="pagination-list ">
          <li>
            <a href="" class="pagination-link is-current">{{ page }}</a>
          </li>
        </ul>
        <a class="pagination-next" v-on:click="changedPage(page + 1)">Siguiente</a>
      </nav>
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
      page: 1,
      pages: 1,
    };
  },
  created() {
    this.fecth();
  },
  methods: {

    fecth() {

      const params = {
        page: this.page
      }

      let result = axios
        .get("https://rickandmortyapi.com/api/character/", { params })
        .then((res) => {
          this.characters = res.data.results;
          this.pages = res.data.info.pages;
        });
    },
    changedPage(page) {
      this.page = (page <= 0 || page > this.pages) ? this.page : page;
      this.fecth();
    }
  },

};
</script>

