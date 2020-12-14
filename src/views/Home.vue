<template>
  <div class="home">
    <h1>{{ message }}</h1>
    {{ products[7]}}
    <div v-for="product in products">
      <img v-bind:src="product.image_url" v-bind:alt="product.name">
    <h2>{{ product.name }} </h2>
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
  },
};
</script>