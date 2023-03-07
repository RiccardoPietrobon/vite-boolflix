<script>
import HeaderSearch from "./components/HeaderSearch.vue";
import OneCard from "./components/OneCard.vue";
import axios from 'axios';
import { store } from "./components/data/store";


export default {
  data() {
    return {
      store,
      endpointFilm: "https://api.themoviedb.org/3/search/movie?api_key=f250a823cd8f88dfcb87039a549a57d3",
      endpointSeries: "https://api.themoviedb.org/3/search/tv?api_key=f250a823cd8f88dfcb87039a549a57d3",
    }
  },

  created() {
    this.fetchCards(this.endpointFilm, this.endpointSeries);
  },

  methods: {

    fetchCards(urlFilm, urlSerie) {
      axios
        .get(urlFilm)
        /* prendo la richiesta */
        .then((responseFilm) => {
          /* riempio l'array */
          store.arrayFilms = responseFilm.data.results;
          console.log(responseFilm.data.results);
        })

      axios
        .get(urlSerie)
        /* prendo la richiesta */
        .then((responseSerie) => {
          /* riempio l'array */
          store.arraySeries = responseSerie.data.results;
          console.log(responseSerie.data.results);
        })

    },
    fetchFiltered(term) {
      this.fetchCards(`${this.endpointFilm}&query=${term}`, `${this.endpointSeries}&query=${term}`);
    },

  },

  components: { HeaderSearch, OneCard },

};
</script>

<template>
  <div class="header bg-dark d-flex">
    <div class="d-flex flex-column flex-md-row container p-2 justify-content-between align-items-center">
      <h1 class="text-danger">BOOLFLIX</h1>
      <HeaderSearch @on-search="fetchFiltered" placeholder="Cerca" />
    </div>
  </div>

  <div class="main bg-dark">
    <div class="container p-5">

      <div v-if="store.arrayFilms.length"> <!-- se l'array è pieno -->

        <h2 class="text-danger">Film</h2>
        <!-- box films -->
        <div class="row row-cols-2 row-cols-md-3 row-cols-lg-5">
          <OneCard v-for="singleFilm in store.arrayFilms" :titolo="singleFilm.title"
            :titoloCer="singleFilm.original_title" :lingua="singleFilm.original_language"
            :valutazione="singleFilm.vote_average" :img="singleFilm.poster_path" />
        </div>

      </div>

      <div v-if="store.arraySeries.length"> <!-- se l'array è pieno -->

        <h2 class="text-danger">Serie</h2>
        <!-- box series -->
        <div class="row row-cols-2 row-cols-md-3 row-cols-lg-5">
          <OneCard v-for="singleSerie in store.arraySeries" :titolo="singleSerie.name"
            :titoloCer="singleSerie.original_name" :lingua="singleSerie.original_language"
            :valutazione="singleSerie.vote_average" :img="singleSerie.poster_path" />
        </div>

      </div>

      <div v-if="!store.arrayFilms.length && !store.arraySeries.length">
        <h2 class="text-danger">
          Inizia con Boolflix
        </h2>
        <p class="text-light">Ricerca i tuoi film o serieTV preferite nella barra di ricerca</p>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.header {
  height: 15vh;
  border-bottom: 2px solid #dc3545;
}

.main {
  height: 85vh;
  overflow: auto;
}
</style>