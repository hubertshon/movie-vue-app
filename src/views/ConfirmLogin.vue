<template>
  <div class="confirm-login">
    <h4> {{message}} </h4>
  </div>
</template>
<style scoped>
.confirm-login {
  height: 24em;
}

h4 {
  margin-top: 5em;
  font-size: 1.5em;
  text-align: center;
}
</style>
<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "You have logged in"
    };
  },
  methods: {}
};
</script>