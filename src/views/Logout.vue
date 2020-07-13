<template>
  <div class="logout">
    <p>You have been logged out</p>
  </div>
</template>

<style scoped>
.logout {
  text-align: center;
  font-size: 2em;
  height: 12em;
}
</style>
<script>
import axios from "axios";

export default {
  created: function() {
    delete axios.defaults.headers.common["Authorization"];
    localStorage.removeItem("jwt");
    this.$router.push("/logout");
  }
};
</script>