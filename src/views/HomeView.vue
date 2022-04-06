<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <h2>{{ message2 }}</h2>
    <div v-for="product in products" :key="product.id">{{ product }}</div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      message: "Welcome to Vue.js!",
      message2: "Everything you could ever not know you wanted!",
      products: [
        {
          id: 1,
          name: "Product 1",
          price: 10,
        },
        {
          id: 2,
          name: "Product 2",
          price: 230,
        },
      ],
    };
  },
  created: function () {},
  methods: {},
};
</script>

<style></style>
