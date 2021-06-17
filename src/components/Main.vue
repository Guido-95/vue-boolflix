<template>
  <div>
    <!-- riga per le tessere -->
    <div v-if="oggettoRicerca.length > 0" class="riga">
      <!-- tessere ciclate -->
      <Tessera v-for="tesseraSingola,indicatore in oggettoRicerca" :key="indicatore" :tessera = tesseraSingola />
      <!-- /tessere ciclate -->
    </div>
    <!-- -riga per le tessere -->

    <!-- testo alternativo se il main è vuoto -->
    <div v-else class="testo-alternativo"> 
      <h2 v-if="oggettoRicerca.length == 0 && statoRicerca == false"> 
        Scrivi un titolo...
      </h2>
      <h2 v-else class="ricerca-fallita"> 
        <span> La tua ricerca non ha prodotto risultati ! </span> 
      </h2> 
    </div>
    <!-- /testo alternativo se il main è vuoto -->
  </div>
</template>

<script>
// import
import Tessera from './Tessera.vue'

export default {
  name:'Main',
  components:{
    Tessera
  },
  props:{
    // props passata da App
    oggettoRicerca:Array,
    statoRicerca:Boolean
  },
  
}
</script>

<style lang="scss" scoped>

  .riga {
    margin: auto;
    text-align: center;
    width: 98%;
    display: flex;
    flex-wrap: wrap;
    justify-content: flex-start;
 
  }

  .testo-alternativo {
    height: calc(100vh - 80px);
    width: 100%;
    display: flex;
    text-transform: uppercase;
    justify-content: center;
    align-items: center;
    background-image: url(../assets/background.png);
   
    h2 {
      font-size: 40px;
      padding: 20px;
      border-radius: 15px;
      background-color: rgba(0,0,0, 0.8);
    }
    .ricerca-fallita {
      font-size: 30px;
      background-color: rgba(0,0,0, 0.8);
      color: red;
    }
  }
</style>