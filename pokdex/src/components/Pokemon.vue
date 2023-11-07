<template>
    <div class="pokemon">
        <div class="card">
            <div class="card-image">
                <figure class="image is-128x128">
                    <img :src="poke.pokePosFront ? poke.pokeFront : poke.pokeBack " alt="Placeholder image">
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                    <div class="media-content">
                        <p class="title is-4"> {{ num }} {{ pokemon }}</p>
                        <p class="subtitle is-6">{{ poke.pokeType }}</p>
                        <button class="button is-small is-info" :onclick="this.alterPokePos">{{ this.poke.pokePosFront ? 'Mostrar de Costa': 'Mostrar de Frente'}}</button>
                    </div>
                </div>
                <div class="content">
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";
    export default {
        name: 'PokemonDescription',
        
        computed: {
            pokemon() {
                return this.name[0].toUpperCase() + this.name.substring(1); 
            },

        },
        created () {
            axios.get(this.url)
            
                .then((res) => {
                    this.description = res.data
                    this.poke.pokeType = res.data.types[0].type.name;
                    this.poke.pokeFront = res.data.sprites.front_default;
                    this.poke.pokeBack = res.data.sprites.back_default;
                })
            
                .catch(error => console.log(error));
        },
        methods: {
            alterPokePos() {
                this.poke.pokePosFront = !this.poke.pokePosFront;
            }
        },
        data () {
            return {
                description: [],
                poke: {
                    pokeType: {},
                    pokeFront: '',
                    pokeBack: '',
                    pokePosFront: true,
                }
            }
        },
        props: {
            num: Number,
            name: String,
            url: String,
            },
        }
</script>

<style scoped>
    .pokemon{
        margin-bottom: 2%;
        box-shadow: 4px 3px 4px rgba(231, 5, 5, 0.726);
    }
    .card{
        display: flex;
        align-items: center;
        justify-content: center;
        background: linear-gradient(to bottom, white, rgba(221, 221, 221, 0.726));
    }
    .image{
        margin: 8%;
        background: linear-gradient(to bottom, #ffffff, #00ff00);
    }
    .card-image{
        height: 80%;
    }
</style>