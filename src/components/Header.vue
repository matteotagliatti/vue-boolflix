<template>
  <form @submit.prevent="$emit('search', searchValue)">
    <input
      type="text"
      placeholder="Search for a movie or show"
      v-model="searchValue"
    />
    <input type="submit" value="Search" />
  </form>
</template>

<script>
export default {
  name: "HeaderDiv",
  data() {
    return {
      searchValue: "",
    };
  },
};
</script>

<style></style>
