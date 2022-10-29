<template>
  <div class="wrapper">
    <h1>Products</h1>
    <div class="section">
      <products-list />
    </div>
  </div>
</template>

<script>
import ProductsList from '../components/ProductsList.vue';
export default {
  name: 'ProductsView',
  components: { ProductsList }
};
</script>

<style scoped>
.wrapper {
  margin: 24px;
}

.section {
  padding: 16px;
  background-color: white;
  border-radius: 8px;
}
</style>
