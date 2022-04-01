<template>
  <div id="app">
    <HeaderDiv @search="searchMoviesOrSeries" />
    <div v-if="movies">
      <h2>Movies</h2>
      <div class="grid">
        <MovieCard v-for="movie in movies" :key="movie.id" :movieData="movie" />
      </div>
    </div>
    <div v-if="tvseries">
      <h2>Tv Series</h2>
      <div class="grid">
        <SerieCard
          v-for="(serie, index) in tvseries"
          :serieData="serie"
          :key="index"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import HeaderDiv from "./components/Header.vue";
import MovieCard from "./components/MovieCard.vue";
import SerieCard from "./components/SerieCard.vue";

export default {
  name: "App",
  components: {
    MovieCard,
    HeaderDiv,
    SerieCard,
  },
  data() {
    return {
      search: "",
      movies: null,
      tvseries: null,
    };
  },
  methods: {
    searchMoviesOrSeries(searchValue) {
      this.search = searchValue;
      // Get Movies
      axios
        .get(
          `https://api.themoviedb.org/3/search/movie?api_key=${process.env.VUE_APP_APIKEY}&query=${this.search}`
        )
        .then((response) => {
          this.movies = response.data.results;
        });
      // Get TV Series
      axios
        .get(
          `https://api.themoviedb.org/3/search/tv?api_key=${process.env.VUE_APP_APIKEY}&query=${this.search}`
        )
        .then((response) => {
          this.tvseries = response.data.results;
        });
    },
  },
};
</script>

<style lang="scss">
@import "./assets/style/style.scss";
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@300;500;600;700&display=swap");
</style>
