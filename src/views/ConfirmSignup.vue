<template>
  <div class="confirm-signup">
    <p> {{message}} </p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "Thank you for signing up!"
    };
  },
  methods: {}
};
</script>