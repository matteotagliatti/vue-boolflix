<template>
  <div>
    <img
      :src="`http://image.tmdb.org/t/p/w185${serieData.poster_path}`"
      :alt="serieData.name"
    />
    <ul>
      <li>{{ serieData.name }}</li>
      <li>{{ serieData.original_name }}</li>
      <li><span :class="selectFlag"></span></li>
      <li>{{ selectVote }}</li>
    </ul>
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
