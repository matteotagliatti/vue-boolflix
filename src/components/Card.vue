<template>
  <div>
    <ul>
      <li>{{ movieData.title }}</li>
      <li>{{ movieData.original_title }}</li>
      <li><span :class="selectFlag()"></span></li>
      <li>{{ movieData.vote_average }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "MovieCard",
  data() {
    return {
      flag: null,
    };
  },
  props: ["movieData"],
  methods: {
    selectFlag() {
      if (this.movieData.original_language === "it") {
        return "fi fi-it";
      } else if (this.movieData.original_language === "en") {
        return "fi fi-us";
      } else {
        return "fi fi-xx";
      }
    },
  },
};
</script>

<style lang="scss" scoped></style>
