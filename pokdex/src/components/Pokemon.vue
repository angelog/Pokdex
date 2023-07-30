<template>
    <div class="pokemon">
        <div class="card">
            <div class="card-image">
                <figure class="image is-128x128">
                    <img :src="poke.pokeFront" alt="Placeholder image">
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                    <div class="media-content">
                        <p class="title is-4"> {{ num }} {{ pokemon }}</p>
                        <p class="subtitle is-6">{{ poke.pokeType }}</p>
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
        data () {
            return {
                description: [],
                poke: {
                    pokeType: {},
                    pokeFront: '',
                    pokeBack: '',
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
    }
    .image{
        background-color: rgba(209, 202, 202, 0.7);
        box-shadow: 0 0 0 4px black;
        margin: 8%;
    }
    .card-image{
        height: 80%;
    }
</style>