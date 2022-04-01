<template>
  <div id="app">
    <HeaderDiv @search="searchMoviesOrSeries" />
    <div class="grid" v-if="movies">
      <div>
        <h1>Movies</h1>
        <MovieCard
          v-for="(movie, index) in movies"
          :movieData="movie"
          :key="index"
        />
      </div>
      <div>
        <h1>TV Series</h1>
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
          console.log(this.tvseries);
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

  .grid {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
  }
}
</style>
