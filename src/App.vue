<template>
  <div id="app">
    <!-- <app-intro v-show="loadingIntro"/> -->
    <header>
      <h1>Boolflix</h1>
      <app-search @performSearch="search" />
    </header>
    <main>   
      <app-grid :items="movies" :loader="loading"/>
      <app-grid :items="series" :loader="loadingSeries"/>
    </main>
  </div>
</template>

<script>
// import AppIntro from './components/AppIntro.vue';
import AppGrid from './components/AppGrid.vue'
import AppSearch from './components/AppSearch.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    // AppIntro,
    AppSearch,
    AppGrid
  },
  data(){
    return{
      apiKey: 'e99307154c6dfb0b4750f6603256716d',
      apiPath: 'https://api.themoviedb.org/3/search/',
      movies:[],
      series:[],
      // loadingIntro: false,
      loading: false,
      loadingSeries: false
    }
  },
  methods:{
    getMovies(queryParams){
      axios.get(this.apiPath+'movie', queryParams).then((res)=>{
        console.log(res.data.results)
        this.movies = res.data.results;
        //this.loadingIntro = false;
        this.loading = false;
      }).catch((error)=>{
        console.log(error);
      })
    },
    getSeries(queryParams){
      axios.get(this.apiPath+'tv', queryParams).then((res)=>{
        this.series = res.data.results;
        //this.loadingIntro = false;
        this.loadingSeries = false;
      }).catch((error)=>{
        console.log(error);
      })
    },
    search(text){
      const queryParams = {
        params:{
          api_key: this.apiKey,
          query: text.split(' ').join('-'),
          language: 'it-IT'
        },
      }
      //this.loadingIntro = true;
      this.loading = true;
      this.loadingSeries = true;
      this.getMovies(queryParams);
      this.getSeries(queryParams);
    }
  },
  // beforeCreate(){
  //   this.loadingIntro = true;
  //   setTimeout(this.loadingIntro = false, 10000);
  // }
}
</script>

<style lang="scss">
@import './styles/general.scss';
h1,
h2{
  text-transform: uppercase;
  color: $base-color;
}
</style>
