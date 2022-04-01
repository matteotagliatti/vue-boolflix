<template>
  <div>
    <img
      :src="`http://image.tmdb.org/t/p/w185${serieData.poster_path}`"
      :alt="serieData.name"
    />
    <ul>
      <li>{{ serieData.name }}</li>
      <li>{{ serieData.original_name }}</li>
      <li><span :class="selectFlag()"></span></li>
      <li>{{ serieData.vote_average }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "SerieCard",
  props: ["serieData"],
  methods: {
    selectFlag() {
      if (this.serieData.original_language === "it") {
        return "fi fi-it";
      } else if (this.serieData.original_language === "en") {
        return "fi fi-us";
      } else {
        return "fi fi-xx";
      }
    },
  },
};
</script>

<style lang="scss" scoped></style>
