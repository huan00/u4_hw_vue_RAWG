<template>
  <div class="card">
    <div class="image-wrapper">
      <!-- Image Goes Here -->
      <img v-bind:src="genre.image_background" alt="img">

    </div>
    <div class="info-wrapper flex-col">
      <!-- Genre Name Goes Here -->
      <h1>{{genre.name}}</h1>
      <!-- {{console.log(genre)}} -->
      
    </div>
  </div>
</template>

<script>
  export default {
    name: 'GenreCard',
    props: {genre: Object}
    
  }
</script>
