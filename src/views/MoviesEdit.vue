<template>
  <div class="movie-edit">
    <form v-on:submit.prevent="editMovie()">
      <h2>Edit Movie</h2>
      <input type="text" class="form-control" v-model="movie.title">
      <input type="text" class="form-control" v-model="movie.year">
      <input type="text" class="form-control" v-model="movie.plot">
      <input type="submit" class="btn btn-primary" value="Edit Movie">
    </form>

    <button v-on:click="deleteMovie()">Delete Movie</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      movie: {},
      errors: []
    };
  },
  created: function() {
    this.showMovie();
  },

  methods: {
    showMovie: function() {
      axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
        console.log(response.data);
        this.movie = response.data;
      });
    },

    editMovie: function() {
      var params = {
        title: this.movie.title,
        year: this.movie.year,
        plot: this.movie.plot
      };

      axios
        .patch(`/api/movies/${this.movie.id}`, params)
        .then(response => {
          this.$router.push(`/movies/${response.data.id}`);
        })
        .catch(error => {
          this.errors = error.response.data.errors;
        });
    },

    deleteMovie: function() {
      axios.delete(`/api/movies/${this.movie.id}`).then(response => {
        console.log("Movie Deleted", response.data);
        this.$router.push("/movies");
      });
    }
  }
};
</script>