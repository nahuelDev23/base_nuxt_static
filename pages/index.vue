<template>
  <div class="container mx-auto grid grid-cols-9 gap-1">
    <div class='flex items-center flex-col bg-gray-700 text-gray-100 text-xl rounded p-4 ' v-for="(pkm,index) in pokemons" :key="'poke'+index">
      <div class="mb-4">{{pkm.name}}</div>
      <img :src="'https://pokeres.bastionbot.org/images/pokemon/' + pkm.id + '.png'" alt="">
    </div>
  </div>
  
</template>

<script>
import axios from "axios";
export default {
  name:'index',
  data() {
    return{
      pokemons:[],
      url:'https://pokeres.bastionbot.org/images/pokemon/'
    }
  },
  
  methods:{
    async fetchData(){
      const allPokemon = await axios.get('https://pokeapi.co/api/v2/pokemon?limit=151');
      let pkm = await allPokemon.data
      pkm.results.forEach(pokemon => {
        pokemon.id = pokemon.url.split('/').filter(function(part){return !! part}).pop()
        console.log(pokemon.id)
        this.pokemons.push(pokemon)
      });
    }
  },
  created(){
    this.fetchData();
  },

}
</script>

<style>

</style>
