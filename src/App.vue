<template>
  <div id="app">
    <header>
      <h1 class="display-6">Boolflix</h1>
      <app-search @performSearch="search" />
    </header>
    <main>     
      <app-grid :items="movies" title="Movies" :loader="loading"/>
      <app-grid :items="series" title="Series" :loader="loadingSeries"/>
    </main>
  </div>
</template>

<script>
import AppGrid from './components/AppGrid.vue'
import AppSearch from './components/AppSearch.vue'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    AppSearch,
    AppGrid
  },
  data(){
    return{
      apiKey: 'e99307154c6dfb0b4750f6603256716d',
      apiPath: 'https://api.themoviedb.org/3/search/',
      movies:[],
      series:[],
      loading: false,
      loadingSeries: false
    }
  },
  methods:{
    getMovies(queryParams){
      axios.get(this.apiPath+'movie', queryParams).then((res)=>{
        this.movies = res.data.results;
        this.loading = false;
      }).catch((error)=>{
        console.log(error);
      })
    },
    getSeries(queryParams){
      axios.get(this.apiPath+'tv', queryParams).then((res)=>{
        this.series = res.data.results;
        this.loadingSeries = false;
      }).catch((error)=>{
        console.log(error);
      })
    },
    search(text){
      const queryParams = {
        params:{
          api_key: this.apiKey,
          query: text.split(' ').join('-')
        },
      }
      this.loading = true;
      this.loadingSeries = true;
      this.getMovies(queryParams);
      this.getSeries(queryParams);
    }
  }
}
</script>

<style lang="scss">
  @import './styles/general.scss' 
</style>
