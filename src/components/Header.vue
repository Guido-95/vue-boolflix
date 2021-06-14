<template>
    <header>
        <div class="logo">
            <img src="../assets/logo-sito.png" alt="Logo">
        </div>
        <div class="ricerca-bottone">
            <input type="text" v-model="oggettoDellaRicerca" placeholder="Cerca qui..">
            <button @click="cliccaBottoneRicerca" type="submit" value="Submit">
                Cerca 
            </button>
            <!-- <div v-if="risultatoChiamata.length >0" >
                <div v-for="prova in risultatoChiamata" :key="prova.title">
                     {{prova.title}}
                </div>
                
            </div> -->
            <div v-if='2<0'></div>
            <div v-else></div>
           
        </div>
    </header>
</template>

<script>
import axios from 'axios'
export default {

    data(){
        return{
            oggettoDellaRicerca:"",
            risultatoChiamata:[],
        }
    },
    methods:{
        cliccaBottoneRicerca(){
            // film
            axios
                .get('https://api.themoviedb.org/3/search/movie',{ 
                    params:{
                    api_key: "e99307154c6dfb0b4750f6603256716d",
                    query: this.oggettoDellaRicerca,
                    language: 'it-It'
                   
                    }
                })
                .then(
                    (risposta) => {
                    this.risultatoChiamata = risposta.data.results;
                    console.log(this.risultatoChiamata);
                    this.$emit("inviaOggettoRicerca", this.risultatoChiamata)
                    }
                )
            // serie tv
            axios
            .get('https://api.themoviedb.org/3/search/movie',{ 
                params:{
                api_key: "e99307154c6dfb0b4750f6603256716d",
                query: this.oggettoDellaRicerca,
                language: 'it-It'
                
                }
            })
            .then(
                (risposta) => {
                this.risultatoChiamata = risposta.data.results;
                console.log(this.risultatoChiamata);
                this.$emit("inviaOggettoRicerca", this.risultatoChiamata)
                }
            )
               
        }      
    }

}
</script>

<style lang="scss" scoped>
    header{
        display: flex;
        justify-content: space-between;
        align-items: center;
        height: 80px;
        padding: 0px 50px;
        background-color: black;
    }
    .logo{
        img{
            width: 150px;
        }
    }

    .ricerca-bottone{
        input{
            height: 30px;
            width: 200px;
            margin: 10px;
        }
        button{
            height: 30px;
            width: 50px;
        }
        
    }
</style>