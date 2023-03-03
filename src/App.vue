<script>

import HeaderSearch from './components/HeaderSearch.vue';
import MainPrincipal from './components/MainPrincipal.vue';

export default {
  data() {
    return {
      title: "This is my App",
    };
  },

  components: {
    HeaderSearch, MainPrincipal
  },
};
</script>

<template>
  <HeaderSearch />
  <MainPrincipal />
</template>

<style lang="scss" scoped></style>
