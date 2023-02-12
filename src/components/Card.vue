<template>
    <div >
        <nav class="inputSearchPokemon">
          <input v-model="searchPokemon" placeholder="Search Pokemon (name or id)"/>        
        </nav> 
        <div class="container">
        <div v-for="pokemon in filteredPokemons()" :key="pokemon.name">
            <div class="card">
                <div class="information">
                    <p class="number">#0{{getId(pokemon)}}</p>
                    <p class="name">
                    {{pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1)}}
                    </p>
                    <button @click="openDetails(getId(pokemon))" class="detailsButton">Details</button>
                </div>
                <div>
                    <img class="pokemonImage" 
                    :alt="`${pokemon.name} image`"
                    :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/${getId(pokemon)}.png`"
                    />
                </div>
        <img class="pokeball" alt="Pokeball logo" src="@/assets/pokeball.png" />
            </div>


            <!-- Pokemon details window -->
            <div @click="closeDetails()" class="bgDetailsBox" v-if="showPokemonDetails"></div>
            <div @click="closeDetails()" class="detailsBox" :style="{backgroundColor: getTypeColor(pokemonDetails.types[0].type.name)}" v-if="showPokemonDetails">   
                
                <div class="detailsInfo">
                    <h1 class="detailsName"> {{pokemonDetails.name.charAt(0).toUpperCase() + pokemonDetails.name.slice(1)}}</h1>
                    <div class="types" v-for="typePokemon in pokemonDetails.types" :key="typePokemon.type.slot">
                        {{typePokemon.type.name.charAt(0).toUpperCase() + typePokemon.type.name.slice(1)}}
                    </div>
                </div>

            <div class="boxStatsMoves">
                <h2 class="statsMovesName">Base stats</h2>
                <div class="statsMovesInfo" v-for="stat in pokemonDetails.stats" :key="stat.stat.name">
                      <p class="statInfoName">
                        {{stat.stat.name.charAt(0).toUpperCase() +
                          stat.stat.name.slice(1)}}:
                      </p>
                      <p>{{stat.base_stat}}</p>
                </div>
            </div>

            <div class="boxStatsMoves">
                <h2 class="statsMovesName">Moves</h2>
                <div class="statsMovesInfo" v-for="move in limitMoves()" :key="move.move.name">
                    <p class="statMoveInfoName">
                        {{move.move.name.charAt(0).toUpperCase() +
                          move.move.name.slice(1)}}
                    </p>
                </div>
            </div>

            <div class="imagesDetailContainer">
                <img class="imageDetail" :src="`${pokemonDetails.sprites.front_default}`"/>
                <img class="imageDetail" :src="`${pokemonDetails.sprites.back_default}`" />
            </div>

            <img class="pokeballDetails" alt="Pokeball logo" src="@/assets/pokeball.png" />
    </div>
    </div>
</div>

</div>

  </template>
  
  <script>
  import { defineComponent } from 'vue';
  import { pokeApi } from '../services/pokeApi';
  
  export default defineComponent ({
    name: "Homepage",
    data() {
        return {
          pokemons: [],
          pokemonDetails: [],
          showPokemonDetails: false,
          searchPokemon: ""
      }
    },
    methods: {
        filteredPokemons(){
        return this.pokemons.filter((pokemon)=>{
          return pokemon.name.includes(this.searchPokemon) || pokemon.url.split("/")[6].includes(this.searchPokemon)
        })
      },
      getId(pokemon){
        return Number(pokemon.url.split("/")[6])
      },
    openDetails(id){
        pokeApi.get(`/pokemon/${id}`).then((resp)=>{
          this.pokemonDetails = resp.data
        })
        this.showPokemonDetails = true
      },
    closeDetails(){
        this.showPokemonDetails = false
      },
      getTypeColor(type){
        switch (type) {
            case 'grass':
            return '#70B873'  
            case 'fire': 
            return '#FF9D55'
            case 'water':
            return '#33A4F5'  
            case 'poison':
            return '#AD61AE'  
            case 'flying':
            return '#6892B0'   
            case 'bug':
            return '#91C12F'  
            case 'normal':
            return '#919AA2' 
            case 'dark':
            return '#5C5365'   
            case 'dragon':
            return '#0A6CBF'   
            case 'ghost':
            return '#8B4E8C'   
            case 'electric':
            return '#F8D030'   
            case 'ground':
            return '#E0C068'   
            case 'fairy':
            return '#EE99AC' 
            case 'ice':
            return '#98D8D8'            
            case 'steel':
            return '#B8B8D0' 
            case 'fighting':
            return '#CE4069'  
            case 'psychic':
            return '#F85888' 
            case 'rock':
            return '#729F92'                         
            default:
            return '#000000'
        }
      },
      limitMoves(){
        return this.pokemonDetails.moves.filter((move, i)=>{
          return i < 6
        })
      }
    },
    mounted() {
        pokeApi.get("/pokemon?limit=21").then((resp) => this.pokemons = resp.data.results)
      }
  })
  </script>

  <style>

  .container {
    display: flex;
        justify-content: center;
        flex-wrap: wrap;
        gap: 2vw;
        margin-top: 4vh;
        background-color: antiquewhite;
        padding-top: 40px;
  }

  .inputSearchPokemon {
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #000000;
    height: 50px;
  }

  input {
    width: 20vw;
    height: 2vh;
    border: none;
    border-radius: 8px;
    padding: 8px;
    text-align: center;
  }

    .card {
        padding: 28px;
        min-width: 320px;
        max-width: 400px;
        border-radius: 12px;
        display: flex;
        position: relative;
        margin: 30px;
        color: #ffffff;
        background-color: lightcoral;
    }

    .number {
        font-size: 16px;
        font-weight: 600;
        text-align: left;
    }

    .name {
        font-size: 32px;
        font-weight: 700;
        letter-spacing: 0em;
        text-align: left;
        margin-bottom: 10px;
    }

    .pokeball {
        position: absolute;
        top: 0;
        right: 0;
    }

    .pokemonImage {
        width: 193px;
        height: 193px;
        position: absolute;
        top: -60px;
        right: 0;
        z-index: 1;
    }

    .detailsButton {
        margin-right: 40px;
        width: 100px;
        height: 30px;
        border: 0;
        background: #33b1f5;
        border-radius: 8px;
        cursor: pointer;
        font-size: 16px;
        font-weight: 700;
        color: #ffffff;
    }

    .bgDetailsBox {
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: 100vh;
        background-color: #000000;
        opacity: 0.8;
        z-index: 2;
    }

    .detailsBox{
        width: 90vw;
        height: 90vh;
        position: fixed;
        top:4%;
        left: 4%;
        border-radius: 8px;
        display: flex;
        gap: 20px;
        z-index: 2;
    }

    .detailsName {
        margin: 2vw 4vw 2vw 4vw;
    }

    .types {
        margin: 0.8vw 0vw 0vw 4vw;
        background-color: #F3EFE0;
        width: 8vw;
        height: 2vw;
        border-radius: 16px;
        font-size: large;
        display: flex;
        align-items: center;
        justify-content: center;
        color: #434242;
        font-weight: 700;
    }

    .imagesDetailContainer {
        display: flex;
        flex-direction: column;
        position: absolute;
        top: 0;
        right: 0;
        z-index: 2;
    }

    .imageDetail {
        width: 22vw;
    }

    .boxStatsMoves {
        display: flex;
        flex-direction: column;
        background-color: #ffffff;
        width: 20vw;
        height: 60vh;
        border-radius: 16px;
        margin-top: 4vw;
    }

    .statsMovesName {
        margin-left: 16px;
    }

    .statsMovesInfo {
        margin-left: 40px;
        display: flex;
        gap: 16px;
    }

    .statInfoName {
        font-weight: 700;
    }

    .pokeballDetails {
        position: absolute;
        top: 0;
        right: 0;
        width: 50vw;
    }

</style>