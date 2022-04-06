<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>{{ message2 }}</h2>
    <div v-for="product in products" :key="product.id">
      {{ product.id }}
      {{ product.name }}
      <img :src="product.image_url" :alt="product.title" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      message2: "Everything you could ever not know you wanted!",
      products: [],
    };
  },
  created: function () {
    this.indexProducts();
  },
  methods: {
    indexProducts: function () {
      axios.get("http://localhost:3000/products.json").then((response) => {
        this.products = response.data;
        console.log("All products", this.products);
      });
    },
  },
};
</script>

<style>
img {
  width: 250px;
}
</style>
