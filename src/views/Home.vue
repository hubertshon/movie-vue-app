<template>
  <div class="home">
    <h2>{{ message }}</h2>
    <p>This is the movie app for Actualize</p>

  </div>
</template>
<style scoped>
.home {
  padding: 7em;
  margin-bottom: 170px;
  text-align: center;
}

.home h2 {
  font-size: 1.5em;
  color: darkslategray;
  line-height: 9vh;
}
</style>


<script>
import axios from "axios";
export default {
  data: function() {
    return {
      message: "Movies!",
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
