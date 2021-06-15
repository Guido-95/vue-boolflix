<template>
    <header>
        <div class="logo">
            <a href="index.html">
                <img src="../assets/logo-sito.png" alt="Logo">
            </a>
            <ul>
                <li class="Home">
                    <a href="index.html"> Home </a> 
                </li>
                <li>
                    Serie TV
                </li>
                <li>
                    Film
                </li>
                <li>
                    Popolari
                </li>
                <li>
                    La mia Lista
                </li>
            </ul>
            
        </div>
        
        <div class="ricerca-bottone">
            <input type="text"  @keyup.enter="cliccaBottoneRicerca" v-model="oggettoDellaRicerca" placeholder="Cerca qui..">
            
            <i @click="cliccaBottoneRicerca" class="fas fa-search"></i>
           <ul>
               <li class="caps"> bambini</li>
               <li><i class="fas fa-bell"></i></li>
               <li class="avatar"> <img src="../assets/avatar.png" alt=""></li>
           </ul>
         
           
        </div>
        
    </header>
</template>

<script>
import axios from 'axios'
export default {

    data(){
        return{
            oggettoDellaRicerca:"",
            movies:[],
            series:[]
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
                    language: 'it-IT'
                   
                    }
                })
                .then(
                    (risposta) => {
                    
                    this.movies = risposta.data.results;
                    this.$emit("inviaFilms", this.movies)
                    this.oggettoDellaRicerca="";
                    }
                )
             
            axios
            .get('https://api.themoviedb.org/3/search/tv',{ 
                params:{
                api_key: "e99307154c6dfb0b4750f6603256716d",
                query: this.oggettoDellaRicerca,
                language: 'it-IT'

                }
            })
            .then(
                (risposta) => {
                this.series = risposta.data.results; 
                this.$emit("inviaSeries", this.series);

                }
            )
           
        },
        
    }

}
</script>

<style lang="scss" scoped>
    header{
        position: fixed;
        top: 0;
        z-index: 1000;
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        height: 80px;
        padding: 0px 50px;
        
        // background-color: transparent;
        background-color: #1b1b1b;
    }
    .logo {
        width: 50%;
        display: flex;
        align-items: center;
        justify-content: space-between;
        a {
            
            display: flex;
            align-items: center;
            justify-content: center;
            
        }
        ul {
            display: flex;
            width: 100%;
           
            list-style: none;
            li {
              margin-right: 15px;
               cursor: pointer;  
            }
            a {  
                text-decoration: none;
                color: white;
            }
        }
        img{
            margin-right: 30px;
            width: 150px;
        }
    }

    .ricerca-bottone{
      
        width: 50%;
        display: flex;
        align-items: center;
        justify-content: flex-end;
        ul {
            
            display: flex;
            align-items: center;
            width: 30%;
            justify-content: space-around;
            
            list-style: none;
        li {
            
            cursor: pointer;
            margin-right: 0px;
            .fa-bell{
                font-size: 25px;
            }  
        }
       
        }
        .avatar{
           
            img{
                border-radius: 5px;
            }
        }
        input{
            border-radius: 10px;
            padding: 10px;
            width: 400px;
            font-size: 20px;
            color: white;
            background-color: #0e0e0e;
        }

         input::placeholder{
             padding: 10px;
             font-size: 20px;
             color: white;
            
            
        }
        .fa-search{
            margin: 0px 25px;
            cursor: pointer;
            font-size: 25px;
        }

        .caps{
            text-transform: uppercase;
        }
        
      
    }
</style>