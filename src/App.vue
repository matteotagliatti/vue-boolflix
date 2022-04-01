<template>
  <div id="app">
    <HeaderDiv @search="searchMoviesOrSeries" />
    <div v-if="movies">
      <h2 v-if="movies.length > 0">Movies</h2>
      <h2 v-esle>No movies found</h2>
      <div class="grid">
        <ItemCard v-for="movie in movies" :key="movie.id" :itemData="movie" />
      </div>
    </div>
    <div v-if="tvseries">
      <h2 v-if="movies.length > 0">Tv Series</h2>
      <h2 v-else>No tv series found</h2>
      <div class="grid">
        <ItemCard
          v-for="(serie, index) in tvseries"
          :itemData="serie"
          :key="index"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import HeaderDiv from "./components/Header.vue";
import ItemCard from "./components/ItemCard.vue";

export default {
  name: "App",
  components: {
    ItemCard,
    HeaderDiv,
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
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@300;500;600;700&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: "Inter", sans-serif;
  padding: 3rem;
  color: black;
  background-color: #f8f9ff;

  h2 {
    color: #565656;
    margin-bottom: 1.5rem;
  }

  .grid {
    display: grid;
    grid-template-columns: repeat(4, minmax(0, 1fr));
    gap: 2rem;
    margin-bottom: 4rem;
  }
}
</style>
