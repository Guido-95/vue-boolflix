<template>
  <div id="app">

    <!-- header -->
    <Header @inviaFilms = catturaFilms
            @inviaSeries = catturaSeries
            />
    <!-- /header -->

    <!-- main -->
    <Main :oggettoRicerca = serieEfilms />
    <!-- /main -->
  </div>
</template>

<script>
// import
import Header from './components/Header.vue'
import Main from './components/Main.vue'

export default {

  name: 'App',
  components: {
    Header,
    Main
  },
  data(){
    return{
      filmsRicevuti:[],
      seriesRicevute:[],
      serieEfilms:[],
    }
   
  },
  methods:{
    // quando l'emit invia l'array dei film
    catturaFilms(films){
      this.filmsRicevuti = films;
      this.unisciArray();
      
    },
    // quando l'emit invia l'array delle serie tv
    catturaSeries(series){
      this.seriesRicevute = series;
      this.unisciArray();
    },
    //  unisci array film e serie
    unisciArray(){
      this.serieEfilms = this.filmsRicevuti.concat(this.seriesRicevute);
    }
      
  }
}
</script>

<style lang="scss">
  @import '~@fortawesome/fontawesome-free/css/all.min.css';

  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }
  
  body{

    font-family: 'Roboto', sans-serif;
    background-color: #1b1b1b;
    color: white;

  }
</style>
