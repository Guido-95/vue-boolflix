<template>
  <div>

    <div class="riga">
      <Tessera  v-for="prova,indicatore in oggettoRicerca" :key="indicatore" :tessera = prova />
    </div>
     <!-- <div class="riga">
      <Tessera v-for="oggetto,indicatore in oggettoRicerca" :key="indicatore" :tessera='oggettoRicerca'/>
    </div> -->


    <!-- <ul>

      <li v-for="oggetto,indicatore in oggettoRicerca" :key="indicatore">
        <h2 v-if="oggetto.title != null "> 
          {{oggetto.title}} 
        </h2>

        <h2 v-else >
          {{oggetto.name}}
        </h2>

        <ul>
          <li v-if="oggetto.title != null ">
            {{oggetto.original_title}}
          </li>
          <li v-else>
            {{oggetto.original_name}}
          </li>
          
          <li v-if="oggetto.original_language== 'it'">
            <img src="../assets/images/it.png" alt="Italiano">
          </li>
          <li v-else-if="oggetto.original_language=='en'">
            <img src="../assets/images/en.png" alt="Inglese">
          </li>
          <li v-else >
            {{oggetto.original_language}}
          </li>
          <li> -->
            <!-- <span v-for="stella,indicatore in stelline" :key="indicatore">
              <i v-if="stella == 'a' " class="fas fa-star"></i>
              <i v-else  class="far fa-star"></i>
            </span> -->
            <!-- {{Math.round((oggetto.vote_average / 2)}} -->
            <!-- {{riempiStelline(Math.round((oggetto.vote_average / 2)))}} -->
            <!-- <span v-for="stellina,indicatore in riempiStelline(Math.round((oggetto.vote_average / 2)))" :key="indicatore" > 
              <i v-if="stellina == 'piena' " class="fas fa-star"></i>
              <i v-else  class="far fa-star"></i> 
            </span> 
          </li>
        </ul> 

      </li>

    </ul> -->
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