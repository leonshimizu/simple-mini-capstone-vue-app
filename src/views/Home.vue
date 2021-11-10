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
        {{ product.id }}
        {{ product.name }}
        <button v-on:click="showFunction(product)">Show More Info</button>
        <button v-on:click="updateFunction">Update Product</button>
        <button v-on:click="deleteFunction">Delete Product</button>
      </li>
    </ol>
    <dialog id="show-product">
      <form method="dialog">
        <!-- {{ currentProduct }} -->
        <p>Name: {{ currentProduct.name }}</p>
        <p>Price: {{ currentProduct.price }}</p>
        <p>Description: {{ currentProduct.description }}</p>
        <p>Supplier ID: {{ currentProduct.supplier_id }}</p>
        <button>Close</button>
      </form>
    </dialog>
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
      supplier_id: "Supplier ID",
      currentProduct: {}
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
    },
    updateFunction: function() {
      console.log("in the update function");
      axios
        .patch('http://localhost:3000/products/229', {
          name: "Update Check"
        })
          .then(response => {
            console.log(response.data);
          })
    },
    deleteFunction: function() {
      console.log("in the delete function");
      axios 
        .delete('http://localhost:3000/products/228')
          .then(response => {
            console.log(response.data);
          })
    },
    showFunction: function(theProduct) {
      console.log(theProduct);
      this.currentProduct = theProduct;
      console.log("in the show function");
      document.querySelector("#show-product").showModal()
    }
  }
};
</script>