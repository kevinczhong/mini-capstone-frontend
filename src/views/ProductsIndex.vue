<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Products",
      products: [],
    };
  },
  created: function () {
    this.indexProducts();
  },
  methods: {
    indexProducts: function () {
      axios.get("/products.json").then((response) => {
        console.log(response.data);
        this.products = response.data;
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div v-for="product in products" v-bind:key="product.id">
      <h2>{{ product.name }}</h2>
      <p>{{ product.images[1].url }}</p>
      <img v-bind:src="product.images[1].url" />
      <p>{{ product.price }}</p>
      <p>{{ product.description }}</p>
      <p><button v-on:click="$router.push(`/products/${product.id}`)">More Details</button></p>
    </div>
  </div>
</template>

<style></style>
