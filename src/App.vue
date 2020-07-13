<template>
  <div id="app">
    <section id="header" class="wrapper">
      <h1>{{ message }}</h1>
      <nav id="nav">
          <ul>
						<li><a href="/">Home</a></li>
            <li><a href="/login">Login</a></li>
            <li><a href="/logout">Logout</a></li>
            <li><a href="/signup">Signup</a></li>
						<li><a href="/movies">Movies</a></li>
          </ul>
        </nav>
    </section>
  <router-view/>
  


		<section id="footer" class="wrapper">
      <div class="title">Footer</div>
      <div class="container">
        <header class="style1">
          <h2>This is the Movie App</h2>
          <p>
            The most random movies curated in one place.
          </p>
        </header>

        <div id="copyright">
          <ul>
            <li>&copy; Untitled.</li><li>Design: <a href="http://html5up.net">HTML5 UP</a></li>
          </ul>
        </div>
      </div>
    </section>
  </div>
</template>

<style>
h1 {
  color: white;
  font-size: 4em;
}

#footer {
  background-color: #e97770;
  color: white;
}

#footer .title {
  background-color: #e97770;
}

#footer .style1 p {
  color: white;
}
</style>

<script>
import axios from "axios";

export default {
  created: function() {
    // delete axios.defaults.headers.common["Authorization"];
    // localStorage.removeItem("jwt");
    // this.$router.push("/logout");
  },
  data: function() {
    return {
      message: "Movie Vue App"
    };
  },

  methods: {
    isLoggedIn: function() {
      return localStorage.getItem("jwt");
    }
  }
};
</script>