<template>
  <div id="app">
    <Header @inviaOggettoRicerca = catturaOggettoRicerca />

    <Main :oggettoRicerca = oggettoDellaRicerca />
   
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
      oggettoDellaRicerca:[],
    }
   
  },
  methods:{
    catturaOggettoRicerca(oggettoRicercaInput){
      this.oggettoDellaRicerca = oggettoRicercaInput;
      
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
    color: grey;
  }


</style>
