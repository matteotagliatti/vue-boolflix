<template>
  <div class="grid-item">
    <div class="overlay"></div>
    <img
      :src="`http://image.tmdb.org/t/p/w185${movieData.poster_path}`"
      :alt="movieData.title"
    />
    <div class="text">
      <div>
        <p class="title">{{ movieData.title }}</p>
        <p class="og-title">
          Original title: <span>{{ movieData.original_title }}</span>
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
  name: "MovieCard",
  props: ["movieData"],
  computed: {
    selectFlag() {
      if (this.movieData.original_language === "it") {
        return "fi fi-it";
      } else if (this.movieData.original_language === "en") {
        return "fi fi-us";
      } else {
        return "fi fi-xx";
      }
    },
    selectVote() {
      const vote = this.movieData.vote_average;
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

<style lang="scss" scoped>
.grid-item {
  position: relative;

  .overlay {
    display: none;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.7);
    border-radius: 2rem;
  }

  img {
    height: 15rem;
    width: 100%;
    height: auto;
    object-fit: cover;
    border-radius: 2rem;
    box-shadow: rgba(0, 0, 0, 0.35) 0px 5px 15px;
  }

  .text {
    display: none;
    padding: 2rem;
    position: absolute;
    bottom: 0;
    color: white;
    gap: 1rem;

    .title {
      font-size: 1.5rem;
      font-weight: bold;
    }

    .og-title {
      font-size: 0.8rem;

      span {
        font-weight: bold;
      }
    }

    .icons {
      display: flex;
      gap: 1rem;

      .stars {
        color: gold;
      }
    }
  }
}

.grid-item:hover .overlay {
  display: block;
}

.grid-item:hover .text {
  display: flex;
  flex-direction: column;
}
</style>
