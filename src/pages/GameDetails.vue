<template>
  <div class="game-content">
    <section v-if='gameDetails' class="image-container">
      <div>
        <img :src="gameDetails.background_image" alt="img">
      </div>
    </section>
    <section v-if="gameDetails" class="details">
      <div class="flex-row space"></div>
      <div>
        <h3>{{gameDetails.name}}</h3>
      </div>
    </section>
  </div>
</template>

<script>
import axios from 'axios'
  export default {
    name: 'GameDetails',
    data: () => ({
      API_KEY: process.env.VUE_APP_RAWG_KEY,
      gameDetails: null
    }),
    mounted() {this.getGameDetails()},
    methods: {
      async getGameDetails() {
        // Get game id from router here
        const res = await axios.get(`https://api.rawg.io/api/games/${this.$route.params.game_id}?key=${this.API_KEY}`)
        this.gameDetails = res.data
      }
    }
  }
</script>
