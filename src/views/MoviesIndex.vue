<template>
  <div class="movie-index">
    <h1>{{ message }}</h1>
    Search by title: <input v-model="titleFilter" list="titles">
    <datalist id="titles">
        <option v-for="movie in movies">{{ movie.title }}</option>
    </datalist>

    <p>Sorted by <b>{{ order }}</b></p><button v-on:click="toggleOrder()">Toggle Sort</button>

    <div v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), order)">
      <h3>Title: {{ movie.title }}</h3>
      <p>Year: {{ movie.year }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <router-link :to="`/movies/${movie.id}`">More Info</router-link>
    </div>

  </div>
</template>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";
export default {
  mixins: [Vue2Filters.mixin],
  data: function() {
    return {
      message: "Movie Vue App",
      movies: [],
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      currentMovie: "",
      titleFilter: "",
      order: "year"
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
    },

    toggleOrder: function() {
      if (this.order === "title") {
        this.order = "year";
      } else {
        this.order = "title";
      }
    }
  }
};
</script>
