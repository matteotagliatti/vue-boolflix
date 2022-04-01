<template>
  <div>
    <ul>
      <li>{{ movieData.title }}</li>
      <li>{{ movieData.original_title }}</li>
      <li>{{ movieData.original_language }}</li>
      <li>{{ movieData.vote_average }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "MovieCard",
  props: ["movieData"],
};
</script>

<style lang="scss" scoped></style>
