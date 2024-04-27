<template>
    <div id="product-wrapper" class="w-full max-w-4xl mx-auto grid grid-cols-2 sm:grid-cols-3 xl:grid-cols-4 gap-6 place-content-center p-4">
      <!-- Product cards will be rendered here -->
      <ProductCard v-for="product in products" :key="product.name" :product="product" @addToCart="updateCart" />
    </div>
  </template>
  
  <script>
  import ProductCard from './ProductCard.vue'
  
  export default {
    props: ['products'],
    components: {
      ProductCard
    },
    methods: {
      updateCart(productName, isAdded) {
        this.$emit('addToCart', productName, isAdded);
      }
    }
  }
  </script>
  