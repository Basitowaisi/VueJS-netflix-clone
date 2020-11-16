<template>
  <Nav />
  <Banner />
  <Row
    :title="row.title"
    :url="row.url"
    v-for="row in rows"
    :key="row.url"
    :isLargeRow="row.isLargeRow"
  />
</template>

<script>
import Nav from "./components/Nav.vue"
import Banner from "./components/Banner.vue"
import Row from "./components/Row.vue"

const base_url = "https://api.themoviedb.org/3"
const API_KEY = process.env.VUE_APP_TMDB_KEY
export default {
  name: "App",
  components: {
    Nav,
    Banner,
    Row,
  },
  data() {
    return {
      rows: [],
    }
  },
  mounted() {
    this.rows = [
      {
        title: "NetFlix Originals",
        url: `${base_url}/discover/tv?api_key=${API_KEY}&with_network=213`,
        isLargeRow: true,
      },
      // {
      //   title: "Trending Now",
      //   url: `${base_url}/trending/all/week?api_key=${API_KEY}&language=en-US`,
      //   isLargeRow: false,
      // },
      {
        title: "Top Rated",
        url: `${base_url}/movie/top_rated?api_key=${API_KEY}&language=en-US`,
        isLargeRow: false,
      },
      {
        title: "Action Movies",
        url: `${base_url}/discover/movie?api_key=${API_KEY}&with_genres=28`,
        isLargeRow: false,
      },
      {
        title: "Comedy Movies",
        url: `${base_url}/discover/movie?api_key=${API_KEY}&with_genres=35`,
        isLargeRow: false,
      },
      {
        title: "Horror Movies",
        url: `${base_url}/discover/movie?api_key=${API_KEY}&with_genres=27`,
        isLargeRow: false,
      },
      {
        title: "Romance Movies",
        url: `${base_url}/discover/movie?api_key=${API_KEY}&with_genres=10749`,
        isLargeRow: false,
      },
      {
        title: "Documentaries",
        url: `${base_url}/discover/movie?api_key=${API_KEY}&with_genres=99`,
        isLargeRow: false,
      },
    ]
  },
}
</script>
