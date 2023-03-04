<script>
import HeaderSearch from "./components/HeaderSearch.vue";
import OneCard from "./components/OneCard.vue";
import axios from 'axios';
import { store } from "./components/data/store";


export default {
  data() {
    return {
      store,
      endpoint: "https://api.themoviedb.org/3/search/movie?api_key=f250a823cd8f88dfcb87039a549a57d3",
    }
  },

  methods: {
    fetchCards(url) {
      axios
        .get(url)
        /* prendo la richiesta */
        .then((response) => {
          /* riempio l'array */
          store.cardsarray = response.data.results;
          console.log(response.data.results);
          //console.log(response.data.results[response.data.results.length - 1]);
        })

    },
    fetchFiltered(term) {
      this.fetchCards(`${this.endpoint}&query=${term}`);
    },

  },

  created() {
    this.fetchCards(this.endpoint);
  },

  components: { HeaderSearch, OneCard },

};
</script>

<template>
  <div class="header bg-dark">
    <div class="d-flex container p-5 justify-content-between">
      <h1 class="text-danger">BOOLFLIX</h1>
      <HeaderSearch @on-search="fetchFiltered" placeholder="Cerca" />
    </div>
  </div>

  <!--  :pic="singleCard.card_images[singleCard.card_images.length - 1].image_url" -->

  <div class="main bg-dark">
    <div class="d-flex container p-5">
      <div class="row row-cols-2 row-cols-md-3 row-cols-lg-5">
        <OneCard v-for="singleFilm in store.cardsarray" :titolo="singleFilm.title" :titoloCer="singleFilm.original_title"
          :lingua="singleFilm.original_language" :valutazione="singleFilm.vote_average" />
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