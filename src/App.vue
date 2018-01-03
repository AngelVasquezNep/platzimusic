<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>PLATZIMUSIC</h1>
    <h2>Elige tu pais y ve los artistas del momento</h2>
    <select  v-model="selectedCountry"  >
      <option v-for="country in countries" v-bind:value="country.value">{{country.name}}</option>
    </select>
    <spinner v-show="loading"></spinner>
    <ul>
      <artist v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid"></artist>
    </ul>
    <div class="footer">
      <p>Gracias por visitar PLATZIMUSIC</p>
      <p>By Angel Vásquez</p>
      <a href="https://twitter.com/angelvasqueznep" target="_blank">Twitter</a>
      <a href="https://github.com/AngelVasquezNep" target="_blank">GitHub</a>
    </div>
  </div>
</template>

<script>
import Artist from './components/Artist.vue'
import Spinner from './components/Spinner.vue'
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      artists:[],
      countries:[
        {name:'Mexico', value: 'Mexico'},
        {name:'Rusia', value: 'Russian Federation'},
        {name:'Colombia', value: 'Colombia'},
        {name:'España', value: 'Spain'}
      ],
      selectedCountry:'Mexico',
      loading: true
    }
  },
  components:{
    Artist: Artist,
    Spinner: Spinner
  },
  methods:{
    refreshArtists(){
      const self = this
      this.loading = true
      this.artists = []
      getArtists(this.selectedCountry)
      .then(function(artists){
        self.loading = false
        self.artists = artists
      })
    }
  },
  mounted(){
    this.refreshArtists()
  },
  watch:{
    selectedCountry(){
      this.refreshArtists()
    }
  }
}
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
  *{
    margin: 0;
  }

  h1, h2 {
    font-weight: normal;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  a {
    color: #42b983;
  }
  li img{
    border-radius: 50%;
  }
  select{
    font-size: 1rem;
    margin: 30px 0;
    height: 2rem;
    width: 6rem;
    background: #41B883;
    color: white;
    border-color: #41B883;
  }
  .footer{
    color: white;
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-around;
    padding: 1rem 0;
    background: #35495E;
    height: 150px;
  }
  .footer a{
    text-decoration: none;
  }


</style>
