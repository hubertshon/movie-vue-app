<template>
  <div class="movie-index">
    <div class="sortsearch">
    <h4>Search by title:</h4><input v-model="titleFilter" list="titles">
    <datalist id="titles">
        <option v-for="movie in movies">{{ movie.title }}</option>
    </datalist>

    <p>Sorted by <b>{{ order }}</b></p><button class="style2" v-on:click="toggleOrder()">Toggle Sort</button>
    </div>

    <section id="highlights" class="movie-list" v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), order)">
      <section class="highlight">
        <h3>Title: {{ movie.title }}</h3>
        <p>Year: {{ movie.year }}</p>
        <p>Plot: {{ movie.plot }}</p>
        <router-link :to="`/movies/${movie.id}`">More Info</router-link>
      </section>
    </section>

  </div>
</template>
<style scoped>
.movie-index {
  margin: 3em;
  line-height: 2vh;
}

.movie-list {
  margin: 60px 30px;
}

h3 {
  font-size: 1.5em;
}

.sortsearch {
  margin: auto;
  -ms-align-items: center;
}
</style>
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
