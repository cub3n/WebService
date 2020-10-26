
<template>
    <Page class="page">
    <ActionBar class="action-bar" >
    
                <GridLayout>
                  <StackLayout>
                  <SearchBar hint="Busca un pokemon"  @submit="onSubmit" /> 
                  
                  </StackLayout>       
                </GridLayout>
    </ActionBar>

          <GridLayout>
            <Label id="hole" :text="searchedpokemon" />
            <Label id="hole1" :text="urlpokemon" />  
          </GridLayout>
    </Page>
</template>

<script >
import * as http from "http";
import { SearchBar } from '@nativescript/core';
    export default {
        data() {
            return {
                pokemon: [],
                searchedpokemon: String,
                urlpokemon: String
            };
        },
        mounted() {
          http.getJSON("https://pokeapi.co/api/v2/pokemon/?limit=151").then(result => {
            this.pokemon = result.results;
            this.searchedpokemon = " ";
            this.urlpokemon= " ";
          }, error => {
              console.log(error);
          });
        },
        
        methods: {
            onSubmit(args) {
            var flag = false;
            const searchBar = args.object;
            this.pokemon.forEach(element => {
              if(element.name==searchBar.text){
                  this.searchedpokemon=element.name;
                  this.urlpokemon=element.url;
                  flag = true
              } 
             });
             if(flag==false)
              {
                this.searchedpokemon= "no existe el pokemon"
                this.urlpokemon= " "
              }
            }
        }

        
  }
</script>

<style scoped>
    ActionBar {
        background-image: url("https://www.alfabetajuega.com/wp-content/uploads/2019/04/pokemon-espada-escudo-780x405.png");
        color: #f30303;
    }
    .message {
        vertical-align: center;
        text-align: center;
        font-size: 20;
        color: #333333;
    }
    #busqueda{
      background-color: #113391;
      text-align: center;
    }
    #hole{
       color: #000000;
       text-align: center;
       margin-top: 40%;
       font-size: 20px;
       
    }
    #hole1{
       color: #000000;
       text-align: center;
       margin-top: 50%;
       font-size: 15px;
       
    }
    .search{
        width: 50%;
    }
    .TextField{
      width: 50%;
      height: 50%;
    }
    .myButton.btnBuscar{
      background-color: #07db07;
    }
</style>
