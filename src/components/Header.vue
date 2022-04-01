<template>
  <div>
    <h1>Boolflix<span>.</span></h1>
    <form @submit.prevent="$emit('search', searchValue)">
      <input
        type="text"
        placeholder="Search for a movie or show"
        v-model="searchValue"
        required
      />
      <input type="submit" value="Search" />
    </form>
  </div>
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

<style lang="scss" scoped>
@import "../assets/style/style.scss";

div {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 4rem;

  form {
    display: flex;
    gap: 0.3rem;

    input {
      padding: 0.5rem;
      border: 2px solid $grey;
      border-radius: 0.7rem;
      background-color: transparent;
      color: black;
      font-size: 1rem;
    }

    input[type="submit"] {
      font-weight: 700;
    }
  }

  h1 {
    color: black;

    span {
      color: $red;
    }
  }
}
</style>
