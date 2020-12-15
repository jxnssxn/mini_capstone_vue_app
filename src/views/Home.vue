<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h4>build a proudct</h4>
    <p>name:<input type="text" v-model="name"></p>
    <p>description:<input type="text" v-model="description"></p>
    <p>price:<input type="text" v-model="price"></p>
    <p>image_url:<input type="text" v-model="image_url"></p>
    <p><button v-on:click="createProduct()">new product</button></p>
    {{ products[7]}}
    <div v-for="product in products">
    <h2>{{ product.name }} </h2>
      <img v-bind:src="product.image_url" v-bind:alt="product.name">
       <h2>{{ product.price }} </h2>
    </div>
  </div>
</template>
<style>
</style>
<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      products: [],
      name: "",
      description: "",
      price: "",
      image_url: "",
    };
  },
  created: function () {
    console.log("print");
    this.indexProducts();
  },
  methods: {
    indexProducts: function () {
      console.log("print print");
      axios.get("/api/products").then((response) => {
        console.log(response.data);
        this.products = response.data;
      });
    },
    createProduct: function () {
      console.log("creating product");
      var params = {
        name: this.name,
        price: this.price,
        description: this.description,
        image_url: this.image_url,
      };
      axios.post("/api/products", params).then((response) => {
        console.log(response.data);
        this.products.push(response.data);
      });
    },
  },
};
</script>