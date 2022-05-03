<template>
    <div class="card text-black" style="width: 100%">

        <p>{{pokemonName}}</p>

        <img :src="pokemonImg" alt="" srcset="" class="card-img-top">

        <ul v-for="type in types" :key="type.name">
            <li>{{type.type.name}}</li>
        </ul>

    </div>
</template>
<script>
import axios from "axios";
export default {
    name:'MyPokemon',
    data(){
        return {
            pokemonName:''
        }
    },
    props:{
        pokemon:Object
    },
    methods:{
        async getPokemonData(url=this.pokemon.url){
            const response = await axios.get(url);
            const res = response.data;
            this.pokemonName = res.name;
            this.pokemonImg = res.sprites.back_default;
            this.types = res.types

        }
    },

     
    // methods:{
    // async loadPokemon(url={{pokemon.url}}){
    // const response = await axios.get(url);
    // const res = response.data
    // this.pokemon = res.results
    // }
    // },

    // data(){
    //     return{
    //         name:this.
    //     }
    // },
    created(){
        this.getPokemonData();
    }
   
}
</script>