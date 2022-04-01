<template>
  <div class="grid-item">
    <div class="overlay"></div>
    <img
      :src="`http://image.tmdb.org/t/p/w185${itemData.poster_path}`"
      :alt="itemData.title"
    />
    <div class="text">
      <div>
        <p class="title">{{ itemData.title || itemData.name }}</p>
        <p class="og-title">
          Original title:
          <span>{{ itemData.original_title || itemData.original_name }}</span>
        </p>
      </div>

      <div class="icons">
        <span :class="selectFlag"></span>
        <span class="stars">{{ selectVote }}</span>
      </div>
      <p class="overview">{{ itemData.overview }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "ItemCard",
  props: ["itemData"],
  computed: {
    selectFlag() {
      if (this.itemData.original_language === "it") {
        return "fi fi-it";
      } else if (this.itemData.original_language === "en") {
        return "fi fi-us";
      } else {
        return "fi fi-xx";
      }
    },
    selectVote() {
      const vote = this.itemData.vote_average;
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
