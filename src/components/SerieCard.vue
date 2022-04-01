<template>
  <div class="grid-item">
    <div class="overlay"></div>
    <img
      :src="`http://image.tmdb.org/t/p/w185${serieData.poster_path}`"
      :alt="serieData.title"
    />
    <div class="text">
      <div>
        <p class="title">{{ serieData.name }}</p>
        <p class="og-title">
          Original title: <span>{{ serieData.original_name }}</span>
        </p>
      </div>
      <div class="icons">
        <span :class="selectFlag"></span>
        <span class="stars">{{ selectVote }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "SerieCard",
  props: ["serieData"],
  computed: {
    selectFlag() {
      if (this.serieData.original_language === "it") {
        return "fi fi-it";
      } else if (this.serieData.original_language === "en") {
        return "fi fi-us";
      } else {
        return "fi fi-xx";
      }
    },
    selectVote() {
      const vote = this.serieData.vote_average;
      if (vote < 2) return "★";
      if (vote > 2 && vote < 4) return "★★";
      if (vote > 4 && vote < 6) return "★★★";
      if (vote > 6 && vote < 8) return "★★★★";
      if (vote > 8 && vote <= 10) return "★★★★★";
      return "";
    },
  },
};
</script>

<style lang="scss" scoped></style>
