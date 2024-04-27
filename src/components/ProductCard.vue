<template>
  <div class="item space-y-2">
    <div
      class="bg-gray-100 flex justify-center relative overflow-hidden group cursor-pointer border rounded-xl"
    >
      <img
        :src="product.url"
        :alt="product.name"
        class="w-full h-full object-cover"
      />
      <button
        :class="
          cartStatus == 'Add To Cart' ? 'bg-green-700 text-white' : 'bg-red-700'
        "
        class="status bg-black text-white absolute bottom-0 left-0 right-0 text-center py-2 translate-y-full transition group-hover:translate-y-0"
        @click="toggleCart"
      >
        {{ cartStatus }}
      </button>

    </div>
    <p class="text-sm">{{ product.name }}</p>
    <strong class="text-sm text-orange-300">$ {{ product.price.toLocaleString() }}</strong>
  </div>
</template>

<script>
export default {
  props: ["product"],
  computed: {
    cartStatus() {
      return this.product.addedToCart ? "Remove From Cart" : "Add To Cart";
    },
  },
  methods: {
    toggleCart() {
      this.product.addedToCart = !this.product.addedToCart;
      this.$emit("addToCart", this.product.name, this.product.addedToCart);
    },
  },
};
</script>
