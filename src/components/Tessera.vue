<template>
    <!-- tessera singola -->
    <div  v-if="tessera.poster_path != null"  class="contenitore-tessere">
        <!-- immagine -->
        <img  :src="creaLocandina(tessera.poster_path)" >
        <!-- /immagine -->

        <!-- info film/serie/cartone -->
        <div class="display-none info">
            <!-- nome film -->
            <div v-if="tessera.title != null" class="titolo"> 
                {{tessera.title}} 
            </div>
            <!-- /nome film -->
            <!-- nome serie -->
            <div class="titolo"  v-else> 
                {{tessera.name}}
            </div>
            <!-- /nome serie -->
            <!-- bandiere e lingue -->
            <div class="bandiera" v-if="tessera.original_language == 'it'">
                <img src="../assets/images/it.png" alt="Italiano">
            </div>
            <div class="bandiera" v-else-if="tessera.original_language =='en'">
                <img src="../assets/images/en.png" alt="Inglese">
            </div>
            <div v-else >
                Lingua : {{tessera.original_language}}
            </div>
            <!-- /bandiere e lingue -->

            <!-- stelline del voto -->
            <div class="voto">
                Voto:
                <span v-for="stellina,indicatore in riempiStelline(Math.round((tessera.vote_average / 2)))" :key="indicatore" > 
                    <i v-if="stellina == 'piena' " class="fas fa-star"></i>
                    <i v-else  class="far fa-star"></i> 
                </span> 
            </div>
            <!-- /stelline del voto -->
            <!-- trama tagliata fino a 250 caratteri -->
            <div class="trama">
                Trama : {{tessera.overview.substr(0,250) + "..." }}
            </div>
            <!-- /trama tagliata fino a 250 caratteri -->
        </div>
        <!-- /info film/serie/cartone -->
    </div>
    <!-- /tessera singola -->
</template>
<script>
export default {
     methods:{
    // crea il percorso dell'immagine, percorso standard + dimensione + percorso immagine
    creaLocandina(percorsoImmagine){
      return 'https://image.tmdb.org/t/p/w342' + percorsoImmagine; 
    },
     // metodo che prende in input un voto calcola il numero delle stelline
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
        // props passata da Main
        tessera:Object,  
    },
}
</script>

<style lang="scss" scoped>
    // contenitore tessera
    .contenitore-tessere {
        display: flex;
        flex-direction: column;
        margin:  15px 15px ;
        position: relative;
        width: calc(100% / 5 - 30px);
        cursor: pointer;
        // hover sulla tessera modifica il div in position absolute
        &:hover .info{
            opacity: 90%;
            transition: 0.2s ease;
            background-color: rgba(0,0,0, 0.9);
        }
        // img film/serie/cartoni
        img{
            height: 100%;
        }
        // informazioni
        .info{
            padding: 20px;
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0px;
            left: 0px;
            opacity: 0;
            overflow:hidden;
            
            .titolo{
                text-align: center;
                margin: 10px;
                font-size: 30px;
            }
            .bandiera {
            display: flex;
            justify-content: center;
            
                img {
                    margin: 20px;
                border-radius: 10px;
                width: 70px;
                }
            }
            .trama{
                margin-top: 10px;
                font-size: 20px;
                padding-bottom: 10px;
                
                color: white;
            }
            .voto{
                margin-bottom: 50px;
                text-align: center;
                text-transform: uppercase;
                font-size: 20px;
                .fas{
                    color: yellow;
                }
            } 
        }
        
       

    }

</style>