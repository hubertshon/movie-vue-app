<template>
  <div class="movie-new">
    <h1>{{ message }}</h1>

    <form v-on:submit.prevent="createMovie()">
      Title<input type="text" v-model="newMovieTitle"></input>
      Year<input type="integer" v-model="newMovieYear"></input><br>
      Plot<textarea rows ="4" cols="40" v-model="newMoviePlot"></textarea><br>
      <input type="submit" class="btn btn-primary" value="Create Movie">
    </form>

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

  methods: {
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
          this.$router.push(`/movies/${response.data.id}`);
        })
        .catch(error => {
          console.log(error.response.data.messages);
        });
    }
  }
};
</script>
