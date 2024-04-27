<template>
   <div class="space-y-4 w-full max-w-[10rem]">
<!-- Filter content -->
<h2 class="text-2xl">Filters</h2>
<h3 class="text-xl">Category</h3>
<div class="text-xl space-y-2">
    <div v-for="category in categories" :key="category">
        <input type="checkbox" class="check" :id="category" @change="filterProducts">
        <label :for="category">{{ category }}</label>
      </div>
    </div>
    
</div>
  
</template>

<script>
export default {
  props: ['products'],
  data() {
    return {
      categories: ['cameras', 'smartphones', 'games', 'televisions'],
    }
  },
  methods: {
    filterProducts() {
      const searchTerm = document.getElementById("Search").value.trim().toLocaleLowerCase();
      const checkedCategories = Array.from(document.querySelectorAll(".check"))
        .filter(check => check.checked)
        .map(check => check.id);
      this.$emit('filter', searchTerm, checkedCategories);
    }
  }
}
</script>