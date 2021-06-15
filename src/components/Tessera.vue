
<template>
    <div  v-if="tessera.poster_path != null"  class="contenitore-tessere">
        <img  :src="creaLocandina(tessera.poster_path)" >
        <!--  -->
        <div class="display-none info">
            <div class="titolo"> 
                Titolo: {{tessera.title}} 
            </div>
            <!-- <div class="titolo"  v-else> 
                Titolo: {{tessera.name}}
            </div> -->
            <div class="bandiera" v-if="tessera.original_language == 'it'">
                <img src="../assets/images/it.png" alt="Italiano">
            </div>
            <div class="bandiera" v-else-if="tessera.original_language =='en'">
                <img src="../assets/images/en.png" alt="Inglese">
            </div>
            <div v-else >
                Lingua : {{tessera.original_language}}
            </div>

            <!-- PROBLEMA -->
                <div>
                    <span v-for="stellina,indicatore in riempiStelline(Math.round((tessera.vote_average / 2)))" :key="indicatore" > 
                        <i v-if="stellina == 'piena' " class="fas fa-star"></i>
                        <i v-else  class="far fa-star"></i> 
                    </span> 
                </div>
            <!-- PROBLEMA -->

            <div>
                {{tessera.overview.substr(0,200) + "..." }}
            </div>
        </div>
    </div>
    
    
</template>

<script>
export default {
     methods:{
    
    creaLocandina(percorsoImmagine){
      return 'https://image.tmdb.org/t/p/w342' + percorsoImmagine; 
    },
        riempiStelline(voto){
            let stelline = [];
        
           
            for (let i = 0; i < voto; i++) {
                stelline.push('piena');
              
            }
            for (let i = voto; i < 5; i++) {
                stelline.push('vuota');
        
            }
            return stelline;
        }
    },
    props:{
        tessera:Object,
        
    },

    data(){
        return{

        }
    },
   
}
</script>

<style lang="scss" scoped>
    .contenitore-tessere{
        display: flex;
        flex-direction: column;
        height: 450px;
        margin:  15px 15px ;
        // border: 2px solid red;
        position: relative;
        width: calc(100% / 5 - 30px);
        
        
        &:hover .info{
            display: block;
            
        }

        img{
            height: 100%;
        }
        .info{
            
            padding: 20px;
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0px;
            left: 0px;
            overflow:hidden;
            background-color: rgba(0,0,0, 0.9);

            .titolo{
                font-size: 25px;
            }
  
        }
        .display-none{
           display: none;
        }

        .fas{
            color: yellow;
        }

        .bandiera img {
         
            width: 50px;
           
          
        }
    }
    
</style>