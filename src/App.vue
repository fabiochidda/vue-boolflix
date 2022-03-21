<template>
  <div id="app">

    <div class="search-bar">
      <input type="text" v-model="search" @keyup.enter="searchFunction">
    </div>

    <ul class="container">
      <li class="movie">
        <div class="category-title">
          <h2>Film</h2>
        </div>
        <div class="movie-card" v-for="el in movies" :key="el.id">
          <div class="image">
            <img v-if="el.poster_path" :src="`https://image.tmdb.org/t/p/w342${el.poster_path}`" alt="">
            <img v-else src="https://image.tmdb.org/t/p/w342/wwemzKWzjKYJFfCeiB57q3r4Bcm.png" alt="">
          </div>
          <div class="info">
            <p>Titolo: {{el.title}}</p>
            <p>Titolo Originale: {{el.original_title}}</p>
            <p>Lingua: {{el.original_language}}</p>
            <p>Voto: {{el.vote_average}}</p>
          </div>
        </div>
      </li>

      <li class="tv-shows">
        <div class="category-title">
          <h2>Serie TV</h2>
        </div>
        <div class="tv-shows-card" v-for="el in tvShows" :key="el.id">
          <div class="image">
            <img v-if="el.poster_path" :src="`https://image.tmdb.org/t/p/w342${el.poster_path}`" alt="">
            <img v-else src="https://image.tmdb.org/t/p/w342/wwemzKWzjKYJFfCeiB57q3r4Bcm.png" alt="">
          </div>
          <div class="info">
            <p>Titolo: {{el.name}}</p>
            <p>Titolo Originale: {{el.original_name}}</p>
            <p>Lingua: {{el.original_language}}</p>
            <p>Voto: {{el.vote_average}}</p>
          </div>
        </div>
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
  methods: {
    searchFunction: function() {

      axios.get(`${this.baseURL}/search/movie`, {
        params: {
          api_key: 'df1607d64d3add4c3ecca5022fee5cce',
          query: this.search,
          language: "it-IT"
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

.container {
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
}

.movie-card, .tv-shows-card {
  width: calc(100% / 5);
  padding-bottom: 50px;
}

.movie, .tv-shows {
  display: flex;
  flex-wrap: wrap;
}

.category-title {
  width: 100%;
}

.image {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 342px;
  height: 513px;
}
</style>
