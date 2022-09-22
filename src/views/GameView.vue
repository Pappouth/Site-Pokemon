<template>
    <div v-if="isLoading">
        Pokédex loading...
    </div>
    <div v-else>
        <div v-if="startGame">
            <q-btn v-if="pokemons.length > 0" label="Suivant" v-on:click="getPokemon(); test();" />
            <q-btn v-else label="Terminer" v-on:click="getPokemon(); test();" />
            <pokemon-card
                :imageSource="pokemon[0]['image']"
                :name="'???'"
                :numero="'???'"
                style="max-width: 300px;"
            />
        </div>
        <div v-else>
            <q-btn v-if="pokemons.length <= 0" label="Relancer" v-on:click="loadPokemons();" />
            <q-btn v-else label="lancer" v-on:click="getPokemon()" />
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import PokemonCard from '@/components/PokemonCard.vue';

export default {
    name: "GameView",
    components: { PokemonCard },
    data() {
        return{
            pokemons: [],
            pokemon: [],
            startGame: false,
            isLoading: false
        }
    },
    methods:
    {
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
        },
        getPokemon() {
            if(this.pokemons.length <= 0){
                this.startGame = false;
            }
            else {
                this.startGame = true;

                const pokemonIndex = Math.floor(Math.random() * this.pokemons.length);
                // ----- TENTATIVE 2 ----- (traiter Object)
                this.pokemon = [];
                this.pokemon.push(this.pokemons[pokemonIndex]);


                // ----- TENTATIVE 3 ----- (traiter Array)
                // this.pokemon = [];
                // const pok = this.pokemons[pokemonIndex];
                // const val = Object.values(pok);
                // this.pokemon.push(val);


                this.pokemons.splice(pokemonIndex, 1);
            }
        },
        test() {
            if(this.pokemon[0]){
                // avec Object
                console.log(/*this.pokemon[0]['name'],*/ this.pokemons.length, this.startGame);

                // avec Array
                // console.log(this.pokemon[0][2], this.pokemons.length, this.startGame);
            }
        }
    },
    mounted() {
        this.loadPokemons();
    }
}
</script>