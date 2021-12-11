<template>
  <div>
    <ul>
      <li v-for="item in productList" :key="item.id">
        <product :product="item" />
        <button @click ="buy(item)" >Add to cart</button> 
        <hr>

      </li>
    </ul>
  </div>
</template>

<script>
import product from "./products/Product.vue";
export default {
  components: {
    product,
  },
  props: ["productList"],
  methods: {
      buy(product) {
          this.$emit('addToCart', product)

      }
  }
};
</script>

<style
Product>
</style>