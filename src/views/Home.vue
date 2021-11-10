<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h1>{{ firstMessage }}</h1>
    <button v-on:click="doSomething">Doing Something</button>
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
  methods: {
    doSomething: function() {
      console.log("doing something");
    }
  }
};
</script>