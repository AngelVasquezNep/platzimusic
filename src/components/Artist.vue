<template>
  <li class="artist">
    <img v-bind:src="artist.image[2]['#text']" alt="">
    <h2><a v-bind:href="artist.url" target="_blank">{{artist.name}}</a></h2>
  </li>
</template>

<script>
  export default {
    name:'artist',
    props: ['artist']
  }

</script>

<style scoped>
  li.artist{
    display: inline-block;
    margin: 1.5rem;
  }
</style>







<!-- <li v-for="artist in artists">{{artist.name}}</li> -->
