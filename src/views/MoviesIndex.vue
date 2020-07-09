<template>
  <div class="movie-index">
    <h1>{{ message }}</h1>

    <div v-for="movie in movies">
      <h3>Title: {{ movie.title }}</h3>
      <p>Year: {{ movie.year }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <router-link :to="`/movies/${movie.id}`">More Info</router-link>
    </div>

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

    showMovie: function(movie) {
      console.log(movie);
      this.currentMovie = movie;
    }
  }
};
</script>
