<template>
  <div>
    
    <ul>
      <li v-for="oggetto,indicatore in oggettoRicerca" :key="indicatore">
        <h2 v-if="oggetto.title != null "> {{oggetto.title}} </h2>
        <h2 v-else >{{oggetto.name}}</h2>
        <ul>
          <li v-if="oggetto.title != null ">{{oggetto.original_title}}</li>
          <li v-else>{{oggetto.original_name}}</li>
          
          <li v-if="oggetto.original_language== 'it'"><img src="../assets/images/it.png" alt="Italiano"></li>
          <li v-else-if="oggetto.original_language=='en'"><img src="../assets/images/en.png" alt="Inglese"></li>
          <li v-else >{{oggetto.original_language}}</li>
          <li>{{Math.round(oggetto.vote_average / 2)}}</li>
        </ul>

      </li>
    </ul>
  </div>
</template>

<script>

export default {
  
   props:{
    oggettoRicerca:Array,
  },
  data(){
    return{
    

    }
  },
  methods:{
    
  },
 
  created(){
  
  },
  updated(){
   
  }
}
</script>

<style lang="scss" scoped>
  ul {
    padding: 25px;
    li{
      ul{
        li{ 
          img{
            height: 20px;
            width: 25px;
          }
        }
      }
    }
  }
</style>