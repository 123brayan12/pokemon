<script setup lang="ts">
 import type { Pokemon } from 'env';
 import getPokemonOptions from './api/getPokemonOptions';
 import { ref } from 'vue';
 import Pokemonoptions from './components/Pokemonoptions.vue';
 import PokemonPicture from './components/PokemonPicture.vue';
 

 const pokemonArr = ref<Pokemon[]>([])
 const pokemon = ref<Pokemon>()
 const shownPokemon = ref<boolean>(false)
 const shownAnswer = ref<boolean>(false)
 const message = ref<string>()
 const selectedId = ref<number>()

 const mixPokemonArray =async()=>{
  pokemonArr.value = await getPokemonOptions()
  const randomInt = Math.floor(Math.random()*4)
  pokemon.value = pokemonArr.value[randomInt]

 }
const checkAnswer =(selectedId: number)=>{
  shownPokemon.value = true
  shownAnswer.value = true

  if(selectedId === pokemon.value?.id ){
     message.value = `Correcto mmgv ya no me voy a romper a tu hermana , eso era ${pokemon.value.name}`
  }
  else{
    message.value = `Mardito gafo de mierda eso era un ${pokemon.value?.name} , Te pareces a frank mmgv `
  }
}


mixPokemonArray()
</script>

<template>
  <div class="m-12">
  <PokemonPicture  v-if="pokemon" :pokemon-id="pokemon.id"/>
  <Pokemonoptions @selection-pokemon="checkAnswer" :pokemons="pokemonArr"/>
  </div>
  <div class="text-center">
    <p class="text-2xl">{{ message }}</p>
  </div>
  
</template>


