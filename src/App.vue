<template>
  <div id="app">

    <div class="search-bar">
      <input type="text" v-model="search">
    </div>

    <div class="movie-container">
      <div class="movie" v-for="el in movies" :key="el.id">
        {{el.title}}
      </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  data() {
    return {
      search: 'men in black',
      movies: []
    }
  },
  created() {
    axios.get(`https://api.themoviedb.org/3/search/movie?api_key=df1607d64d3add4c3ecca5022fee5cce&query=${ this.search }`)
    .then( res => {
      this.movies = res.data.results
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
</style>
