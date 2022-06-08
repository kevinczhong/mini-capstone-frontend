<script>
import axios from "axios";

export default {
  data: function () {
    return {
      productParams: {},
      errors: [],
    };
  },
  created: function () {
    axios.get("/products/" + this.$route.params.id + ".json").then((response) => {
      this.productParams = response.data;
    });
  },
  methods: {
    submit: function () {
      axios
        .patch("/products/" + this.$route.params.id + ".json", this.productParams)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/products/");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="submit">
    <form v-on:submit.prevent="submit()">
      <h1>Edit Product Details</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Name:</label>
        <input type="text" v-model="productParams.name" />
      </div>
      <div>
        <label>Price:</label>
        <input type="text" v-model.number="productParams.price" />
      </div>
      <div>
        <label>Description:</label>
        <input type="text" v-model="productParams.description" />
      </div>
      <div>
        <label>Supplier:</label>
        <input type="text" v-model.number="productParams.supplier_id" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>
