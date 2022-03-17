<template>
  <div id="app">

    <div class="search-bar">
      <input type="text" v-model="search">
    </div>

    <ul class="movie-container">
      <li class="movie" v-for="el in movies" :key="el.id">
        {{el.title}}
        {{el.original_title}}
        {{el.original_language}}
        {{el.vote_average}}
      </li>
    </ul>

  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  data() {
    return {
      search: 'men in black',
      baseURL: 'https://api.themoviedb.org/3',
      movies: [],
      tvShows: []
    }
  },
  created() {
    axios.get(`${this.baseURL}/search/movie`, {
      params: {
        api_key: 'df1607d64d3add4c3ecca5022fee5cce',
        query: this.search,
        language: 'it-IT'
      }
    })
    .then( res => {
      this.movies = res.data.results
    })
    .catch( error => {
      console.log(error.response)
    })

    axios.get(`${this.baseURL}/search/tv`, {
      params: {
        api_key: 'df1607d64d3add4c3ecca5022fee5cce',
        query: this.search,
        language: "it-IT"
      }
    })
    .then( res => {
      this.tvShows = res.data.results
    })
    .catch( error => {
      console.log(error.response)
    })
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

ul li {
  list-style: none;
}

.movie-container {
  display: flex;
  flex-wrap: wrap;
}

.movie {
  width: calc(100% / 5);
  padding-bottom: 50px;
}
</style>
