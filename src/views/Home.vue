<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h1>{{ firstMessage }}</h1>
    <button v-on:click="doSomething">Doing Something</button>
    <hr>
    <h2>Here are all the Products:</h2>
    <button v-on:click="createFunction">Create Product</button>
    <p><input type="text" v-model="name"></p>
    <p><input type="text" v-model="price"></p>
    <p><input type="text" v-model="description"></p>
    <p><input type="text" v-model="supplier_id"></p>
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
      products: [],
      name: "Name",
      price: "Price",
      description: "Description",
      supplier_id: "Supplier ID"
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
    },
    createFunction: function() {
      console.log("in the create function");
      axios
        .post('http://localhost:3000/products', {
          name: this.name,
          price: this.price,
          description: this.description,
          supplier_id: this.supplier_id
        }).then(response => {
          console.log(response.data);
          this.products.push(response.data);
        })
    }
  }
};
</script>