<template>
  <div class="confirm-login">
    <p> {{message}} </p>
  </div>
</template>

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