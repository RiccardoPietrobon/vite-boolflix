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
    this.fetchCardsFilms(this.endpointFilm);
    this.fetchCardsSeries(this.endpointSeries);
  },

  methods: {
    fetchCardsFilms(url) {
      axios
        .get(url)
        /* prendo la richiesta */
        .then((response) => {
          /* riempio l'array */
          store.arrayFilms = response.data.results;
          console.log(response.data.results);
        })

    },
    fetchFilteredFilms(term) {
      this.fetchCardsFilms(`${this.endpointFilm}&query=${term}`);
    },


    fetchCardsSeries(url) {
      axios
        .get(url)
        /* prendo la richiesta */
        .then((response) => {
          /* riempio l'array */
          store.arraySeries = response.data.results;
          console.log(response.data.results);
        })

    },
    fetchFilteredSeries(term) {
      this.fetchCardsSeries(`${this.endpointSeries}&query=${term}`);
    },

  },

  components: { HeaderSearch, CardFilms, CardSeries },

};
</script>

<template>
  <div class="header bg-dark">
    <div class="d-flex container p-5 justify-content-between">
      <h1 class="text-danger">BOOLFLIX</h1>
      <HeaderSearch @on-search="(fetchFilteredFilms, fetchFilteredSeries)" placeholder="Cerca" />
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