<template>
    <header :class="{ 'onScroll': !view.topOfPage}">
        <div class="logo">
            <a href="index.html">
                <img src="../assets/logo-sito.png" alt="Logo">
            </a>
            <ul >
                <li class="Home">
                    <a href="index.html"> Home </a> 
                </li>
                <li class="serie-tv">
                    Serie <span class="tv"> TV </span> 
                </li>
                <li class="film">
                    Film
                </li>
                <li class="popolari">
                    Popolari
                </li>
                <li class="la-mia-lista">
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
                <li class="avatar"> 
                    <img src="../assets/avatar.png" alt="avatar"> 
                    <i class="fas fa-caret-down">
                        <div class="menu-avatar">
                            <ul class="menu-comparsa top">
                                <li><img src="../assets/bambini.png" alt="bambini"> <a href=""> bambini </a>  </li>
                                <li><a href=""> Gestici i profili </a></li>
                            </ul>
                            <ul class="menu-comparsa bottom">
                                
                                <li><a href=""> Account</a></li>
                                <li><a href=""> Centro Assistenza</a></li>
                                <li><a href=""> Esci da Netflix</a></li>
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
        box-shadow: 0 0 2px #aaa;
        background-color: rgb(10, 10, 10);
        }
    }
    .logo {
        
        display: flex;
        align-items: center;
        
        .serie-tv{
            display: flex;
        }
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
            width: 25%;
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
                padding: 30px 0px;
                position: relative;
                margin-left: 10px;
                .menu-avatar{
                    position: absolute;
                    top: 70px;
                    left: -140px;
                    width: 200px;
                   
                    background-color:black ;
                    display: none;
                    .menu-comparsa.top{
                        border-bottom: 1px solid white;
                    }
                    .menu-comparsa{
                        width: 100%;
                        justify-content: center;
                        font-family: 'Roboto', sans-serif;
                        font-weight: 400;
                        display: flex;
                        flex-direction: column;
                        align-items: flex-start;
                        li {
                            font-size: 13px;
                            display: flex;
                            align-items: center;
                            text-align: center;
                            margin: 5px;
                            padding: 10px;
                            img {
                               
                              
                                margin-right: 10px;
                            }
                            a {
                                color: white;
                                text-decoration: none;
                            } 
                        }
                    }
                }
                &:hover .menu-avatar{
                    display: block;
                }
                // &:hover{
                //     transition: 0.2s ;
                //     transform: rotate(180deg);
                // }
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
            margin: 0px 15px;
            cursor: pointer;
            font-size: 25px;
        }

        .caps{
            text-transform: uppercase;
        } 
    }

    @media (min-width: 576px) { 
        .caps{
            display: none;
        } 

        .logo > ul {
            display: none;
        }  
   
    }
    @media (max-width: 575px) { 
        .caps,
        .fa-bell,
        .la-mia-lista,
        .tv,
        .popolari,
        .fa-bell,
        .avatar,
        .fa-caret-down,
        .avatar > img,
        .fa-search{
            display: none;
        } 

        .logo > a > img{
            width: 100px;
        }

        .logo > ul {
            font-size: 12px;
            display: none;
        }  
    }

    @media (min-width: 576px) { 
        .caps,
        .fa-bell,
        .la-mia-lista,
        .tv,
        .popolari,
        .fa-bell,
        .avatar > img ,
        .fa-caret-down{
            display: none;
        } 
        
    }

    // Medium devices (tablets, 768px and up)
    @media (min-width: 768px) { 
        .caps,
        .fa-bell,
        .la-mia-lista,
        .tv,
        .popolari,
        .fa-bell,
        .film{
            display: none;
        }  
        .logo > ul ,
        .avatar > img,
        .fa-caret-down {
            font-size: 13px;
            display: flex;
        }  
    }

    @media (min-width: 992px) { 
        .caps,
        .tv,
        .fa-bell{
            display: none;
        }
        .popolari,
        .avatar > img,
        .fa-caret-down{
            display: block;
        }
        .logo > ul {
            font-size: 14px;
            display: flex;
        }  
    }

     @media (min-width: 1200px) { 
        .caps,
        .fa-bell,
        .tv,
        .popolari,
        .la-mia-lista,
        .avatar > img,
        .fa-caret-down{
            display: block;
        }

        .logo > ul {
            font-size: 18px;
            display: flex;
        }  

    }
</style>