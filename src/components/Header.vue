<template>
    <header :class="{ 'onScroll': !view.topOfPage}">
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
                <li class="avatar"> <img src="../assets/avatar.png" alt=""> 
                    <i class="fas fa-caret-down">
                        <div class="menu-avatar">
                            <ul>
                                <li></li>
                                <li></li>
                                <li></li>
                                <li></li>
                            </ul>
                        </div>
                    </i> 
                </li>
           </ul>
         
           
        </div>
        
    </header>
</template>

<script>
import axios from 'axios'
export default {

    data(){
        return{
            view: {
                topOfPage: true
            },
            oggettoDellaRicerca:"",
            movies:[],
            series:[],
            ricerca : false
        }
    },
    beforeMount() {
        window.addEventListener('scroll', this.handleScroll)
    },
    methods:{
        handleScroll(){
            if(window.pageYOffset > 0 ){
                if(this.view.topOfPage) this.view.topOfPage = false
            } else {
                if(!this.view.topOfPage) this.view.topOfPage = true
            }
        },
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
                    this.movies.forEach(
                        element =>{
                            element.type= "Film";
                        })
                  
                    this.$emit("inviaFilms", this.movies);
                    this.ricerca = true;
                    this.$emit("ricercaFatta", this.ricerca);
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
                this.series.forEach(
                    element =>{
                        element.type= "Serie";
                    })
                    
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
        transition: all 0.4s ease-in-out;  
        // background-color: transparent;
        background-color: transparent;
        &.onScroll {
        transition: all 0.4s ease-in-out;    
        box-shadow: 0 0 5px #aaa;
        background-color: rgb(10, 10, 10);
        }
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
            display: flex;
            align-items: center;
            .fa-caret-down{
                position: relative;
                margin-left: 10px;
                
                &:hover{
                    transition: 0.2s ;
                    transform: rotate(180deg);
                }
            }
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