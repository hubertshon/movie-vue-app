<template>
  <div class="movie-show">
      <h1>{{ movie.title }}</h1>
      <h3>Year: {{ movie.year}}</h3>
      <p>Plot: {{ movie.plot }}</p>
      <router-link :to="`/movies/${movie.id}/edit`">Edit Movie</router-link>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      movie: ""
    };
  },
  created: function() {
    this.showMovie();
  },

  methods: {
    showMovie: function(movie) {
      axios.get(`/api/movies/${this.$route.params.id}`).then(response => {
        console.log(response.data);
        this.movie = response.data;
      });
    }
  }
};
</script>