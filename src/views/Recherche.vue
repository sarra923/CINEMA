<template>
    <div className="recherche">
        <form v-on:submit.prevent="recherche()">
            <div className="input-group">
                <input class="input" type="text" placeholder="Rechercher un film" v-model="uneRecherche">
                <button v-on:click="recherche" class="button is-dark">Rechercher</button>
            </div>
        </form>
        <br>
        <h2>Resultats de la recherche</h2>


        <br>
        <br>

        <div class="resultat">
            <center>
                <table>
                    <tr v-for="unFilm in films" v-bind:key="unFilm.key">
                        <center><td>{{unFilm.title}}
                            <td v-if="unFilm.poster_path!=null" width="200px">
                                <img v-bind:src="'http://image.tmdb.org/t/p/w500' + unFilm.poster_path"></td>
                            <br>
                            </td>
                        </center>
                        <td>
                            <button v-on:click="voirDetails(unFilm)" class="button is-dark">Détails</button>
                        </td>
                    </tr>
                </table>
            </center>
        </div>


    </div>
</template>

<script>
    import axios from 'axios'

    export default {
        name: 'Recherche ',
        data() {
            return {
                baseUrl: 'https://api.themoviedb.org/3/search/movie' ,
                films: [],

                uneRecherche: '',
                api_key: '3f2e73f99471592447bae321c22cd045'
            }
        },
        methods: {
            async recherche(){
                // const response = await axios.get(this.baseUrl + '/search.json?title=${this.query}');
                const response = await axios.get(this.baseUrl + '?api_key=' + this.api_key + '&query=' + this.uneRecherche);
                this.films = await response.data.results;
            },

            voirDetails(film) {
                this.$router.push({
                    path: 'details', query: {
                        id: film.id,
                        titre: film.title
                    }
                });
            }
        }
    }
</script>

<style>
    h2{
        padding: 20px;
        font-size: 19px;

    }



    #app {
        background-color: #35495E;

    }

    input.input{
        width: 25%;
    }


    td:not([align]), th:not([align]) {
        text-align: inherit;
        height: 200px;
    }

    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #ffffff;
    }

    .td{
        color: white;
        height: 200px;
    }

    html{
        background-color: #35495E;
        font-size: 16px;
        -moz-osx-font-smoothing: grayscale;
        -webkit-font-smoothing: antialiased;
        min-height: 969px;
        overflow-x: hidden;
        overflow-y: scroll;
        text-rendering: optimizeLegibility;
        -webkit-text-size-adjust: 100%;
        -moz-text-size-adjust: 100%;
        text-size-adjust: 100%;
    }


    .input-group {
        margin-top: 1rem;
        display: flex;
        justify-content: center;
    }

    .input-group-field {
        margin-right: 0;
    }

    .input-group .input-group-button {
        margin-left: 0;
        border: none;
    }

    .input-group .md-raised {
        margin-top: 0;
        margin-bottom: 0;
        border-radius: 0;
    }
    .button1{
        padding: 15px 100px;
        margin: 10px 4px;
        color: #FFFFFF;
        background-color: mediumvioletred;
        font-family: sans-serif;
        text-transform: uppercase;
        text-align: center;
        position: relative;
        right: 0px;
        bottom:-30px;
        text-decoration: none;
        display: inline-block;
        border: 1px solid;
    }
</style>
