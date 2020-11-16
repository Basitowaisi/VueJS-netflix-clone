<template>
  <div className="row">
    <h2>{{ title }}</h2>
    <div className="row__posters">
      <img
        class="row__poster"
        :class="isLargeRow ? 'row__posterLarge' : ''"
        :src="
          isLargeRow
            ? base_url + movie.poster_path
            : base_url + movie.backdrop_path
        "
        :key="movie.id"
        :alt="movie.name"
        v-for="movie in movies"
        @click="handleClick(movie.name)"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios"
export default {
  props: ["isLargeRow", "url", "title"],
  data() {
    return {
      movies: [],
    }
  },
  mounted() {
    axios
      .get(this.url)
      .then(({ data }) => {
        this.movies = data.results
      })
      .catch((e) => console.log(e))
  },

  computed: {
    base_url() {
      return "https://image.tmdb.org/t/p/original"
    },
  },
}
</script>

<style scoped>
.row {
  margin-left: 20px;
  color: #fff;
}

.row__posters {
  display: flex;
  overflow-y: hidden;
  overflow-x: scroll;
  padding: 20px;
}

.row__posters::-webkit-scrollbar {
  display: none;
}

.row__poster {
  width: 100%;
  object-fit: contain;
  max-height: 100px;
  transition: transform 0.45s;
  margin-right: 10px;
}

.row__poster:hover {
  transform: scale(1.08);
}

.row__posterLarge {
  max-height: 250px;
}
.row__posterLarge:hover {
  transform: scale(1.09);
}
</style>
