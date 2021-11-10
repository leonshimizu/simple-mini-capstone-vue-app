<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h1>{{ firstMessage }}</h1>
    <button v-on:click="doSomething">Doing Something</button>
    <ol>
      <li v-for="product in products" v-bind:key="product.id">
        {{ product }}
      </li>
    </ol>
    <!-- <p>{{ products }}</p> -->
  </div>
</template>

<style></style>

<script>
import axios from 'axios';
export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      firstMessage: "Hello World",
      products: []
    };
  },
  created: function() {
    this.indexFunction();
  },
  methods: {
    doSomething: function() {
      console.log("doing something");
    },
    indexFunction: function() {
      console.log("in the index function");
      axios
        .get('http://localhost:3000/products')
        .then(response => {
          console.log(response.data);
          this.products = response.data;
        });
    }
  }
};
</script>