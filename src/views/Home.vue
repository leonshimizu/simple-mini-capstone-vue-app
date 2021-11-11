<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h1>{{ firstMessage }}</h1>
    <button v-on:click="doSomething">Doing Something</button>
    <hr>
    <h2>Here are all the Products:</h2>
    <ol>
      <li v-for="product in products" v-bind:key="product.id">
        {{ product.id }}
        {{ product.name }}
        <button v-on:click="showFunction(product)">Show More Info</button>
      </li>
    </ol>
    <dialog id="show-product">
      <form method="dialog">
        <p>Name: <input type="text" v-model="currentProduct.name"></p>
        <p>Price: <input type="text" v-model="currentProduct.price"></p>
        <p>Description: <input type="text" v-model="currentProduct.description"></p>
        <p>Supplier ID: <input type="text" v-model="currentProduct.supplier_id"></p>
        <button v-on:click="updateFunction(currentProduct)">Update</button>
        <button v-on:click="deleteFunction(currentProduct)">Delete</button>
        <button>Close</button>
      </form>
    </dialog>
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
    updateFunction: function(theProduct) {
      console.log("in the update function");
      console.log(theProduct.name)
      axios
        .patch('http://localhost:3000/products/' + theProduct.id, {
          name: theProduct.name,
          supplier_id: theProduct.supplier_id
        })
          .then(response => {
            console.log(response.data);
          })
    },
    deleteFunction: function(theProduct) {
      console.log(theProduct.name)
      console.log("in the delete function");
      axios 
        .delete(`http://localhost:3000/products/${theProduct.id}`)
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

//  updateRecipe: function(theRecipe) { // can use params this way as well
//       console.log('updating recipe.....');
//       var recipeEditParams = {
//         title: theRecipe.title,
//         ingredients: theRecipe.ingredients,
//         directions: theRecipe.directions,
//         prep_time: theRecipe.prep_time,
//         image_url: theRecipe.image_url,
//         chef: theRecipe.chef,
//       };
      
//       // axios.patch("http://localhost:3000/recipes/" + theRecipe.id, recipeEditParams).then(response => {
//       axios.patch(`http://localhost:3000/recipes/${theRecipe.id}`, recipeEditParams).then(response => {
//         console.log(response.data);
//       });