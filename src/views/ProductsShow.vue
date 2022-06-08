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
  methods: {},
};
</script>

<template>
  <div class="home">
    <h1>{{ product.name }}</h1>
    <p>{{ product.price }}</p>
    <p>{{ product.description }}</p>
  </div>
</template>

<style></style>
