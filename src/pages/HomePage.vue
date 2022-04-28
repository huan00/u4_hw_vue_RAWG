<template>
  <div>
    <div class="search">
      <!-- Search Form Goes Here -->
      <form @submit="getSearchResults">
        <input type="search" value='' @input="handleChange"/>
        <button>searchQuery</button>
      </form>
      <h2>Search Results</h2>
      <section class="search-results container-grid">
        <GameCard v-for="result in searchResults" :key="result.id" :result="result" @click="selectGame(result.id)" :genre="false"/>
      </section>
    </div>

    <div v-if="searched === false" class="genres">
      <h2>Genres</h2>
      <section class="container-grid">
        
        <GenreCard v-for="genre in genres" :key="genre.id" v-bind:genre="genre" @click="selectGenre(genre.id)" />
      </section>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import GenreCard from '../components/GenreCard.vue'
import GameCard from '../components/GameCard.vue'
  export default {
    name: 'HomePage',
    components:{
      GenreCard,
      GameCard
    },
    data: () => ({
      API_KEY: process.env.VUE_APP_RAWG_KEY,
      genres: [],
      searchQuery: '',
      searchResults: [],
      searched: false
    }),
    mounted() {
      this.getGenres()
    },
    methods: {
      async getGenres() {
        const res = await axios.get(`https://api.rawg.io/api/genres?key=${this.API_KEY}`)
        this.genres = res.data.results

      },
      async getSearchResults(e) {
        e.preventDefault()
        const res = await axios.get(`https://api.rawg.io/api/games?key=${this.API_KEY}&search=${this.searchQuery}`)
        this.searchResults = res.data.results
        console.log(res.data.results)
        this.searched = true
      },
      handleChange(event) {
        this.searchQuery = event.target.value
        console.log(this.searchQuery)
      },
      selectGame(gameId) {
        console.log(gameId)
        this.$router.push(`/details/${gameId}`)
      },
      selectGenre(genreId){
        this.$router.push(`/games/${genreId}`)
      }
    }
  }
</script>
