<template>
  <header class="banner" ref="banner">
    <div class="banner__contents">
      <h1 class="banner__title">
        {{ movie?.title || movie?.name || movie?.original_name }}
      </h1>
      <div class="banner__buttons">
        <button class="banner__button">Play</button>
        <button class="banner__button">My List</button>
      </div>
      <h1 class="banner__description">
        {{ overview }}
      </h1>
    </div>
    <div class="banner--fadeBottom"></div>
  </header>
</template>

<script>
import axios from "axios"
const API_KEY = "5e161de38e79c6f6970b942b82c13a0b"
export default {
  name: "Banner",
  data() {
    return {
      movie: {},
    }
  },
  computed: {
    overview() {
      const n = 150
      return this.movie.overview?.length > n
        ? this.movie.overview.substr(0, n - 1) + "..."
        : this.movie.overview
    },
  },
  created() {
    axios
      .get(
        `https://api.themoviedb.org/3/discover/tv?api_key=${API_KEY}&with_network=213`
      )
      .then(({ data }) => {
        this.movie =
          data.results[Math.floor(Math.random() * data.results.length - 1)]
        this.$refs.banner.style.backgroundImage = `url(https://image.tmdb.org/t/p/original/${this.movie?.backdrop_path})`
      })
      .catch((e) => console.log(e))
  },
}
</script>
<style scoped>
.banner {
  background-size: cover;
  background-position: center center;
  color: #fff;
  background-size: cover;
  height: 448px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.banner__contents {
  margin-left: 38px;
  padding-top: 140px;
  height: 190px;
}

.banner__title {
  font-size: 3rem;
  font-weight: 800;
  padding-bottom: 0.3rem;
}

.banner__description {
  width: 45rem;
  line-height: 1.3;
  padding-top: 1rem;
  font-size: 0.8rem;
  max-width: 360px;
  height: 80px;
}

.banner__button {
  cursor: pointer;
  color: #fff;
  outline: none;
  border: none;
  font-weight: 700;
  border-radius: 0.2vw;
  padding-left: 2rem;
  padding-right: 2rem;
  margin-right: 1rem;
  padding-top: 0.5rem;
  background-color: rgba(51, 51, 51, 0.5);
  padding-bottom: 0.5rem;
  transition: all 0.2s;
}

.banner__button:hover {
  color: #000;
  background-color: #e6e6e6;
}

.banner--fadeBottom {
  height: 7.4rem;
  background-image: linear-gradient(
    180deg,
    transparent,
    rgba(37, 37, 37, 0.61),
    #111
  );
}
</style>
