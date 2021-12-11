<template>
  <div id="app">
    <div v-if="showCart">
      <h2>your cart</h2>
      <h2>cart total items: {{ cart.length }}</h2>
      <ul>
        <li v-for="(item, index) in cart" :key="index">
          {{ item.title }} | {{ item.price }} $
        </li>
      </ul>
      <p>
        total sum:
        {{ cartTotal }}
      </p>
    </div>
    <button @click="showCart = !showCart">
      <span v-if="!showCart">Show cart</span>
      <span v-else>Hide cart</span>
    </button>
    <!-- 1. categories component , 2 categories prop , 3 categories  variable -->
    <categories :categories="cate" @setCategory="setCategory"/>
    <products :productList="filteredProductList" @addToCart="buyProduct" />
  </div>
</template>

<script>
const axios = require("axios");
//import HelloWorld from './components/HelloWorld.vue'

import Categories from "./components/Categories.vue";
import Products from "./components/Products.vue";

export default {
  name: "App",
  components: {
    Categories,
    Products,
    //HelloWorld
  },

  data: () => {
    //remember to add return
    return {
      products: [],
      cate: [],
      cart: [],
      showCart: false,
      selectedCategory: undefined,
    };
  },
  methods: {
    buyProduct(product) {
      this.cart.push(product);
    },
    setCategory(cate){
      this.selectedCategory =cate
    },
  },
  computed: {
    cartTotal() {
      let total = 0;
      for (let index = 0; index < this.cart.length; index++) {
        total += this.cart[index].price;
      }
      return total;
    },
    filteredProductList(){
      if(this.selectedCategory){
        return this.products.filter(item => {
          return item.category === this.selectedCategory
        })

      }else {
        return this.products
      }
      

    },
  },

  //accesss to the api
  mounted() {
    axios
      .get("https://fakestoreapi.com/products")
      .then((results) => {
        this.products = results.data;
      })
      .catch((error) => console.log(error));
    axios
      .get("https://fakestoreapi.com/products/categories")
      .then((results) => {
        this.cate = results.data;
      })
      .catch((error) => console.log(error));
  },
};
</script>


<style>
</style>
