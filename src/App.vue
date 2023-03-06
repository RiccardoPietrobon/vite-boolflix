<script>
import HeaderSearch from "./components/HeaderSearch.vue";
import CardFilms from "./components/CardFilms.vue";
import CardSeries from "./components/CardSeries.vue";
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
        .get(urlFilm, urlSerie)
        /* prendo la richiesta */
        .then((responseFilm, responseSerie) => {
          /* riempio l'array */
          store.arrayFilms = responseFilm.data.results;
          console.log(responseFilm.data.results);

          store.arraySeries = responseSerie.data.results;
          console.log(responseSerie.data.results);

        })

    },
    fetchFiltered(term) {
      this.fetchCards(`${this.endpointFilm}&query=${term}`, `${this.endpointSeries}&query=${term}`);
    },

  },

  components: { HeaderSearch, CardFilms, CardSeries },

};
</script>

<template>
  <div class="header bg-dark">
    <div class="d-flex container p-5 justify-content-between">
      <h1 class="text-danger">BOOLFLIX</h1>
      <HeaderSearch @on-search="fetchFiltered" placeholder="Cerca" />
    </div>
  </div>

  <div class="main bg-dark">
    <div class="d-flex container p-5">
      <div class="row row-cols-2 row-cols-md-3 row-cols-lg-5">
        <CardFilms v-for="singleFilm in store.arrayFilms" :titolo="singleFilm.title"
          :titoloCer="singleFilm.original_title" :lingua="singleFilm.original_language"
          :valutazione="singleFilm.vote_average" />
      </div>
      <div class="row row-cols-2 row-cols-md-3 row-cols-lg-5">
        <CardSeries v-for="singleSerie in store.arraySeries" :titolo="singleSerie.title"
          :titoloCer="singleSerie.original_title" :lingua="singleSerie.original_language"
          :valutazione="singleSerie.vote_average" />
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