<template>
    <div class="flex flex-col items-center mt-14 space-y-4">
    <li @click="$emit('SelectionPokemon',pokemon.id)" class="text-5xl"v-for="pokemon in pokemons" :key="pokemon.id">
    {{ pokemon.name  }}
    </li>
    </div>

</template>
<script lang="ts" setup>
import type { Pokemon } from 'env'

defineProps<{
    pokemons: Pokemon[
    ]
}>()
</script>