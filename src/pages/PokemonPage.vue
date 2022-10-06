<template>
    <h1 v-if="!pokemon">Espere un momento perra...</h1>
    <div v-else>
        <h1>Cual pokemon es?</h1>
        <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon"></PokemonPicture>
        <PokemonOpcion :pokemons = "pokemonArr" @selection="checkAnswer($event)"></PokemonOpcion>
        <template v-if="showAnswer">
            <h2>{{message}}</h2>
            <button class="button-74" @click="newGame">Nuevo juego</button>
        </template>
    </div>
</template>

<script>
import PokemonPicture from '@/components/PokemonPicture.vue';
import PokemonOpcion from '@/components/PokemonOpcion.vue';
import getPokemonOptions from '@/helpers/getPokemonsOptios'



export default {

    components: { PokemonPicture, PokemonOpcion },
    data() {
        return {
            pokemonArr: [],
            pokemon: null,
            showPokemon: false,
            showAnswer:false,
            message:""
        }
    },
    methods:{
        async mixPokemonArry(){
            this.pokemonArr = await getPokemonOptions()

            const rndInt = Math.floor (Math.random() * 4)
            this.pokemon = this.pokemonArr[rndInt]
            console.log(this.pokemon.name)
        },

        checkAnswer(pokemonId){
            this.showPokemon = true
            this.showAnswer = true
            if(pokemonId === this.pokemon.id){
                this.message = `Mero virgen, si es el: ${this.pokemon.name}`
            } else{
                this.message = `Mucho bruto, era el: ${this.pokemon.name}`
                
            }

        },
        newGame(){
            this.pokemonArr= [],
            this.pokemon= null,
            this.showPokemon= false,
            this.showAnswer=false
            this.mixPokemonArry()
        }
    },
    mounted(){
        this.mixPokemonArry()
    }
}
</script>

<style scoped>




/* CSS */
.button-74 {
  background-color: #fbeee0;
  border: 2px solid #422800;
  border-radius: 30px;
  box-shadow: #422800 4px 4px 0 0;
  color: #422800;
  cursor: pointer;
  display: inline-block;
  font-weight: 600;
  font-size: 18px;
  padding: 0 18px;
  line-height: 50px;
  text-align: center;
  text-decoration: none;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

.button-74:hover {
  background-color: #fff;
}

.button-74:active {
  box-shadow: #422800 2px 2px 0 0;
  transform: translate(2px, 2px);
}

@media (min-width: 768px) {
  .button-74 {
    min-width: 120px;
    padding: 0 25px;
  }
}
</style>
