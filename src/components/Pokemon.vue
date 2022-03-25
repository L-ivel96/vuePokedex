<template>
    <div class="card elementoPokemon">
        <div class="card-image">
            <figure class="">
            <img :src="currentImg" :alt="name | FirstUpper">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
                <div class="media-content">
                    <p class="title is-4">{{ num }} - {{ name | FirstUpper }}</p>
                    <p class="subtitle is-6">{{ pokemon.type | FirstUpper }}</p>
                </div>
            </div>
            <div class="content">
                <button class="button is-fullwidth" @click="girarPokemon">Girar Pokemon</button>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    name: "Pokemon",
    created: function() {
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = res.data.sprites.front_default;
        });
    },
    data() {
        return {
            isFront: true,
            currentImg: '',
            pokemon: {
                type: '',
                front: '',
                back: ''
            }
        }
    },
    props: {
        num: Number,
        name: String,
        url: String
    },
    filters: {
        FirstUpper: function(valor) {
            if(valor !== '') {
                let novoValor = valor[0].toUpperCase() + valor.slice(1);
                return novoValor;
            }
            else {
                return valor;
            }
        }
    },
    methods: {
        girarPokemon: function() {
            if(this.isFront) {
                this.isFront = false;
                this.currentImg = this.pokemon.back;
            }
            else {
                this.isFront = true;
                this.currentImg = this.pokemon.front;
            }
        }
    }
}
</script>

<style scoped>
    .elementoPokemon {
        margin-bottom: 1.5em;
        margin-left: 0.5em;
    }

    .title {
        white-space: nowrap;
    }
</style>