<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>{{ message2 }}</h2>

    <div>
      <h1>ADD TO THE PROBLEM</h1>
      <div>DUBBED: <input type="text" v-model="newRecipeParams.name" /></div>
      <div>
        THE SACRIFICE: <input type="text" v-model="newRecipeParams.price" />
      </div>
      <div>
        IS WHAT NOW: <input type="text" v-model="newRecipeParams.description" />
      </div>
      <div>
        SHOW US: <input type="text" v-model="newRecipeParams.image_url" />
      </div>
      <button v-on:click="createProducts">BRING FORTH</button>
    </div>

    <div v-for="product in products" :key="product.id">
      <h2>{{ product.id }}</h2>
      <h1>{{ product.name }}</h1>
      <img :src="product.image_url" :alt="product.title" />
      <br /><button v-on:click="showProduct(product)">More Info!</button>
    </div>
    <dialog id="product-details">
      <form method="dialog">
        <h1>Product Info</h1>
        <p>Name: {{ currentProduct.name }}</p>
        <p>Price: {{ currentProduct.price }}</p>
        <p>Description: {{ currentProduct.description }}</p>
        <p>Image Url: {{ currentProduct.image_url }}</p>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "The Place to do The Things for The Stuff",
      message2: "Everything you could ever not know you wanted!",
      products: [],
      newRecipeParams: {},
      currentProduct: {},
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
    createProducts: function () {
      console.log("MAKE ONE");

      axios
        .post("http://localhost:3000/products.json", this.newRecipeParams)
        .then((response) => {
          console.log("GREAT SUCCESS", response.data);
          this.products.push(response.data);
        })
        .catch((error) => console.log(error.response));
      this.newRecipeParams = {};
    },
    showProduct: function (product) {
      console.log(product);
      this.currentProduct = product;
      document.querySelector("#product-details").showModal();
    },
  },
};
</script>

<style>
img {
  width: 250px;
}
</style>
