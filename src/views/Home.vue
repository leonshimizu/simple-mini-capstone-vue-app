<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h1>{{ firstMessage }}</h1>
  </div>
</template>

<style></style>

<script>
export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      firstMessage: "Hello World"
    };
  },
  created: function() {},
  methods: {}
};
</script>