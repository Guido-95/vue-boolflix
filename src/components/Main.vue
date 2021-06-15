<template>
  <div>

    <div v-if="oggettoRicerca.length > 0" class="riga">
      <Tessera v-for="tesseraSingola,indicatore in oggettoRicerca" :key="indicatore" :tessera = tesseraSingola />
     
    </div>
    <div v-else> <h1> CERCA UN TITOLO.. </h1> </div>
  </div>
</template>

<script>
import Tessera from './Tessera.vue'
export default {
  components:{
    Tessera
  },
  props:{
    oggettoRicerca:Array,
  },
  data(){
    return{
    stelline:[],

    }
  },
  methods:{
    riempiStelline(voto){
      this.stelline=[];
      for (let i = 0; i < voto; i++) {
        this.stelline.push('piena');
      
      }
      for (let i = voto; i < 5; i++) {
        this.stelline.push('vuota');
    
      }
      return this.stelline;
    }
  },
 
  created(){
  
  },
  updated(){
   
  }
}
</script>

<style lang="scss" scoped>
.riga {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  
}
  ul {
    padding: 25px;
    li{
      ul{
        li{ 
          span{
            .fas{
              color: green;
            }
          }
          img{
            height: 20px;
            width: 25px;
          }
        }
      }
    }
  }
</style>