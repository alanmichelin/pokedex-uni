<template>
    <div class="container col-xs-12">
         <div class="row">
            <div :key="pokemon.name" v-for="pokemon in pokemones" class="col-3 mt-4">
                <MyPokemon :pokemon="pokemon" />
            </div>
        </div>
        <button id='atras'>Atras</button>
        <button id='adelante'>Adelante</button>
    </div>
</template>
<script>
import axios from "axios";
import MyPokemon from './Pokemon.vue'
export default {
    name:'MyPokemones',
    data(){
        return{
            pokemones:[],
            nombre:'',
            data:''
        }
    },
    components:{
        MyPokemon
    },
    methods:{
        async loadPokemones(url='https://pokeapi.co/api/v2/pokemon/'){
        const response = await axios.get(url);
        const res = response.data
        this.pokemones = res.results
        this.data = res;
        this.handleButtons();
        },
        handleButtons(){
            document.getElementById('atras').addEventListener('click',()=>{
                console.log('test')
                this.data.previous != null && this.loadPokemones(this.data.previous)
            })
            document.getElementById('adelante').addEventListener('click',()=>{
                this.data.next != null && this.loadPokemones(this.data.next)

            })
        }
    },
    created(){
        this.loadPokemones();
    }
}
</script>