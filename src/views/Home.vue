<template>
  <div class="home">
    <h1>{{ message }}</h1>

    <form>
      Title<input type="text" v-model="newMovieTitle"></input>
      Year<input type="integer" v-model="newMovieYear"></input><br>
      Plot<textarea rows ="4" cols="40" v-model="newMoviePlot"></textarea><br>
      <button v-on:click="createMovie()">New Movie</button>
    </form>

    <div v-for="movie in movies">
      <h3>Title: {{ movie.title }}</h3>
      <p>Year: {{ movie.year }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <button v-on:click="showMovie(movie)">More Info</button>
    </div>

    <dialog id="movie-details">
      <p>Name: <input type="text" v-model="currentMovie.title"></p>
      <p>Year: <input type="text" v-model="currentMovie.year"></p>
      <p>Plot: <input type="text" v-model="currentMovie.plot"></p>
      <p>Genre: {{ currentMovie.genre }}</p>
      <button v-on:click="updateMovie(currentMovie)">Update</button>
      <button v-on:click="deleteMovie(currentMovie)">Delete Movie</button>
    </dialog>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      message: "Movie Vue App",
      movies: [],
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      currentMovie: ""
    };
  },
  created: function() {
    this.indexMovies();
  },
  methods: {
    indexMovies: function() {
      axios.get("/api/movies").then(response => {
        console.log("All Movies", response.data);
        this.movies = response.data;
      });
    },

    createMovie: function() {
      var params = {
        title: this.newMovieTitle,
        year: this.newMovieYear,
        plot: this.newMoviePlot
      };

      axios
        .post("/api/movies", params)
        .then(response => {
          console.log("Success", response.data);
          this.movies.push(response.data);
        })
        .catch(error => {
          console.log(error.response.data.errors);
          this.errors = error.response.data.errors;
        });
    },

    showMovie: function(movie) {
      console.log(movie);
      this.currentMovie = movie;
      document.querySelector("#movie-details").showModal();
    },

    updateMovie: function(movie) {
      var params = {
        title: movie.title,
        year: movie.year,
        plot: movie.description
      };

      axios.patch(`/api/movies/${movie.id}`, params).then(response => {
        console.log("Movie Updated");
      });
    },

    deleteMovie: function(movie) {
      axios.delete(`/api/movies/${movie.id}`).then(response => {
        console.log("Movie Deleted");
      });
      var index = this.movies.indexOf(movie);
      this.movies.splice(index, 1);
    }
  }
};
</script>
