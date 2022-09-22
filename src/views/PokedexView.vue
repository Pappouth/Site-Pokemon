<template>
    <div v-if="isLoading">
        Pokédex loading...
    </div>
    <div v-else class="q-pa-md row q-col-gutter-lg">
        <div class="col-lg-4 col-md-4 col-xs-12 col-sm-12" v-for="pokemon in pokemons" :key="pokemon.id">
        <pokemon-card
            :imageSource="pokemon.image"
            :name="pokemon.name"
            :numero="pokemon.pokedexId"
            :types="pokemon.apiTypes"
        />
        </div>
    </div>
</template>

<script>
import axios from "axios";
import PokemonCard from "@/components/PokemonCard.vue";

export default {
    name: "PokedexView",
    components: { PokemonCard },
    data() {
        return {
            pokemons: [],
            isLoading: false
        }
    },
    methods: {
        loadPokemons() {
            this.isLoading = true;
            axios
                .get("https://pokebuildapi.fr/api/v1/pokemon")
                .then((pokemons) => {
                    this.pokemons = pokemons.data;
                })
                .catch((error) => console.log(error))
                .finally(() => this.isLoading = false)
            ;
        }
    },
    mounted() {
        this.loadPokemons();
    }
}
</script>