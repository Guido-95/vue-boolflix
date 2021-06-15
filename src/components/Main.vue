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
      <h2> 
        Scrivi un titolo...
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
  },
  
}
</script>

<style lang="scss" scoped>

  .riga {
    display: flex;
    flex-wrap: wrap;
 
  }

  .testo-alternativo{
    height: calc(90vh - 80px);
    width: 100%;
    font-size: 35px;
    display: flex;
    text-transform: uppercase;
    justify-content: center;
    align-items: center;
  }
</style>