<script>
import axios from "axios";

export default {
  data: function () {
    return {
      product: [],
    };
  },
  created: function () {
    axios.get("/products/" + this.$route.params.id + ".json").then((response) => {
      this.product = response.data;
    });
  },
  methods: {
    destroyProduct: function () {
      axios.delete("/products/" + this.$route.params.id + ".json").then((response) => {
        console.log("This product has been successfully deleted", response.data);
        this.$router.push("/products/");
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ product.name }}</h1>
    <p>{{ product.price }}</p>
    <p>{{ product.description }}</p>
    <p><button v-on:click="$router.push(`/products/edit/${product.id}`)">Edit this product</button></p>
    <p><button v-on:click="destroyProduct">Delete this product</button></p>
  </div>
</template>

<style></style>
