<template>
  <div>
    <img :src="product.image" alt="product.title" />
    <h2>{{ product.title }}</h2>
    <h3>
      <b>{{ product.price }} $</b>
    </h3>
    <p>{{ product.description }}</p>
    
  </div>
</template>

<script>
export default {
  props: ["product"],
};
</script>


<style scoped>
/*scoped locks this style for just this component */
img {
  max-height: 100px;
}
</style>