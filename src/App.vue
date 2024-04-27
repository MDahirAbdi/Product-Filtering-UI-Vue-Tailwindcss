<template>
  <div class="bg-gray-800 text-white">
    <Navbar :cartItemCount="cartItemCount" @filterProducts="filterProducts" />
    <main class="flex flex-col md:flex-row mx-auto container max-w-6xl">
      <Filters :products="products" @filter="filterProducts" />
      <ProductWrapper :products="filteredProducts" @addToCart="updateCart" />
    </main>
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";
import Filters from "./components/Filters.vue";
import ProductWrapper from "./components/ProductWrapper.vue";

export default {
  components: {
    Navbar,
    Filters,
    ProductWrapper,
  },
  data() {
    return {
      products: [
        {
          name: "Sony Playstation 5",
          url: "../src/assets/images/xbox_series_x.png",
          category: "games",
          price: 499.99,
        },
        {
          name: "Samsung Galaxy",
          url: "../src/assets/images/samsung_galaxy.png",
          category: "smartphones",
          price: 399.99,
        },
        {
          name: "Cannon EOS Camera",
          url: "../src/assets/images/cannon_eos_camera.png",
          category: "cameras",
          price: 749.99,
        },
        {
          name: "Sony A7 Camera",
          url: "../src/assets/images/sony_a7_camera.png",
          category: "cameras",
          price: 1999.99,
        },
        {
          name: "LG TV",
          url: "../src/assets/images/lg_tv.png",
          category: "televisions",
          price: 799.99,
        },
        {
          name: "Nintendo Switch",
          url: "../src/assets/images/nintendo_switch.png",
          category: "games",
          price: 299.99,
        },
        {
          name: "Xbox Series X",
          url: "../src/assets/images/xbox_series_x.png",
          category: "games",
          price: 499.99,
        },
        {
          name: "Samsung TV",
          url: "../src/assets/images/samsung_tv.png",
          category: "televisions",
          price: 1099.99,
        },
        {
          name: "Google Pixel",
          url: "../src/assets/images/google_pixel.png",
          category: "smartphones",
          price: 499.99,
        },
        {
          name: "Sony ZV1F Camera",
          url: "../src/assets/images/sony_zv1f_camera.png",
          category: "cameras",
          price: 799.99,
        },
        {
          name: "Toshiba TV",
          url: "../src/assets/images/toshiba_tv.png",
          category: "televisions",
          price: 499.99,
        },
        {
          name: "iPhone 14",
          url: "../src/assets/images/iphone_14.png",
          category: "smartphones",
          price: 999.99,
        },
      ],
      filteredProducts: [],
      cartItemCount: 0,
      search: "",
      checkList: [],
    };
  },
  watch: {
    filteredProducts: {
      handler(val, old_val) {
        if (this.filteredProducts.length == 0) {
          if (this.checkList?.length == 0 && this.search == "")
            this.filteredProducts = this.products;
        }
      },
      deep: true,
    },
  },
  methods: {
    filterProducts(searchTerm, checked) {
      // Convert the search term to lowercase
      const lowercaseSearchTerm = searchTerm.toLowerCase();
      this.search = searchTerm;
      this.checkList = checked;
      // If no checkboxes are checked, reset the filter to include all products
      // Filter products based on the search term and checked categories
      this.filteredProducts = this.products.filter((product) => {
        // Check if the product name matches the search term
        const matchesSearchTerm = product.name
          .toLowerCase()
          .includes(lowercaseSearchTerm);
        // Check if checked categories are defined and if the product category is included in them
        const isInCheckedCategories =
          checked && checked.includes(product.category.toLowerCase());
        // Return true if the product matches both conditions
        return (
          matchesSearchTerm && (checked === undefined || isInCheckedCategories)
        );
      });
    },
    updateCart(productName, isAdded) {
      if (isAdded) {
        this.cartItemCount++;
      } else {
        this.cartItemCount--;
      }
      localStorage.setItem("itemCount", this.cartItemCount);
      // You can emit an event to update the cart count in Navbar or manage it centrally using Vuex
    },
  },
  beforeMount() {
    this.cartItemCount = localStorage.getItem("itemCount")??0;
    this.filteredProducts = this.products;
  },
};
</script>
