<template>
  <div id="app">
    <HeaderDiv @search="searchMovies" />
    <div v-if="apiData">
      <MovieCard />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import HeaderDiv from "./components/Header.vue";
import MovieCard from "./components/Card.vue";

export default {
  name: "App",
  components: {
    MovieCard,
    HeaderDiv,
  },
  data() {
    return {
      search: "",
      apiData: null,
    };
  },
  methods: {
    searchMovies(searchValue) {
      this.search = searchValue;
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=${process.env.VUE_APP_APIKEY}&query=${this.search}`
        )
        .then((response) => {
          this.apiData = response.data.results;
          console.log(this.apiData);
        });
    },
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  padding: 5rem;
  color: black;
}
</style>
