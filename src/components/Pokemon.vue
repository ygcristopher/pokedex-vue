<template>
    <div id="pokemon-card">
        <div class="card">
            <div class="card-image" id="pokemon-content">
                <figure >
                    <img :src="currentImg" alt="Placeholder image">
                </figure>
            </div>
            <div class="card-content">
                <div class="media">
                    <div class="media-content" id="pokemon-description">
                        <p class="title is-4">{{ num }} {{ upper }} </p>
                        <p class="subtitle is-6">{{ pokemon.type }}</p>
                        <button class="button is-normal" id="btn-change" @click="spriteChangePokemon">Change</button>
                    </div>
                </div>

            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    created: function () {
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.back = res.data.sprites.back_default;
            this.currentImg = this.pokemon.front;
        }).catch(error => {
            console.error('Error fetching data:', error);
        });
    },
    data() {
        return {
            isFront: true,
            currentImg: '',
            pokemon: {
                type:'',
                front: '',
                back: '',
            }
        }
    },
    props: {
        num: Number,
        name: String,
        url: String
    },
    computed: {
        upper: function () {
            var newName = this.name[0].toUpperCase() + this.name.slice(1);
            return newName;
        },
    },
    methods: {
        spriteChangePokemon: function() {
            if(this.isFront){
                this.isFront = false;
                this.currentImg = this.pokemon.back;
            }else {
                this.isFront = true;
                this.currentImg = this.pokemon.front;
            }
        }
    }
    
}
</script>

<style>
    #pokemon-card {
        margin-top: 1rem;
    }

    #pokemon-content {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
    }

    #pokemon-description {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;   
    }

    #btn-change {
        width: 100%;
    }
</style>