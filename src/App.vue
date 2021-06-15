<template>
  <div id="app">
    <Header @inviaFilms = catturaFilms
            @inviaSeries = catturaSeries
            />

    <Main :oggettoRicerca = serieEfilms />
   
  </div>
</template>

<script>
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
    catturaFilms(films){
      this.filmsRicevuti = films;
      console.log("1)this.filmsRicevutiAPP=",this.filmsRicevuti );
      this.unisciArray();
      
    },
    catturaSeries(series){
       this.seriesRicevute = series;
       console.log("2)this.SeriesRicevuteAPP=",this.seriesRicevute );
      this.unisciArray();
      },
      unisciArray(){
        //  unisci array film e serie
        this.serieEfilms = this.filmsRicevuti.concat(this.seriesRicevute);
        console.log("3)this.arrayUnito=",this.serieEfilms );
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
    background-color: #1b1b1b;
  }


</style>
