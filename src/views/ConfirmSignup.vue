<template>
  <div class="confirm-signup">
    <p> {{message}} </p>
  </div>
</template>
<style scoped>
.confirm-signup {
  text-align: center;
  height: 7em;
}
</style>
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