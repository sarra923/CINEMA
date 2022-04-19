<template>
  <div class="accueil">
    <h1>Recherche de films PWA</h1>
    <h2>Rechercher des films populaires</h2>
    <br>
    <br>
    <div class="card">
      <div v-for="unFilm in films.results" v-bind:key="unFilm.key">
        <p v-if="unFilm.poster_path">
        <p class ="color"><b>{{unFilm.title}}</b></p>
        <p class ="color"><b>{{unFilm.vote_average}}/10</b></p>
          <img v-bind:src="'http://image.tmdb.org/t/p/w500' + unFilm.poster_path">
        </p>
        <button v-on:click="voirDetails(unFilm)" class="button is-dark">Détails</button>

        <hr>
      </div>
    </div>
    <br>
    <br>
    <br>
  </div>
</template>



<script>
  import axios from 'axios'

  export default {
    name: 'Accueil',
    data(){
      return{
        films : [],

        api_key: '3f2e73f99471592447bae321c22cd045'
      }
    },

    created(){
      this.recherche();
    },

    methods: {
      async recherche(){
        const response = await axios.get('https://api.themoviedb.org/3/movie/popular?api_key=' + this.api_key + "&language=fr");
        this.films = await response.data;
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
  .card{
    background-color: #35495E;
  }
  .input-group {
    margin-top: 1rem;
    display: flex;
    justify-content: center;
  }
  .color{
    color: #FFFFFF;
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
</style>