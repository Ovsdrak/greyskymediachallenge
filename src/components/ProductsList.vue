<template>
  <search-product @change="filterText = $event"/>
  <product v-for="product in productsFromPage" :product="product">
    <product-form :product="product" />
  </product>
  <div class="paginate-actions">
    <button v-show="currentPage > 1"
            @click="currentPage--"
            class="btn-small">Prev page</button>
    <button v-show="currentPage < totalPages"
            class="btn-small"
            @click="currentPage++">Next page</button>
  </div>
  <div class="table-actions">
    <p>Page <strong>{{ currentPage }}</strong> of <strong>{{ totalPages }}</strong></p>

    <div>
      Sort by
      <select v-model="sortedBy" title="Sort Order">
        <option :value="undefined">Sort Order</option>
        <option value="A-Z">A-Z</option>
        <option value="Created Date">Created Date</option>
      </select>
    </div>

    <select v-model="itemsPerPage" >
      <option :value="10">10</option>
      <option :value="25">25</option>
      <option :value="50">50</option>
      <option :value="100">100</option>
    </select>
  </div>
</template>

<script>
import Product from './Product.vue';
import SearchProduct from './SearchProduct.vue';
import ProductForm from './ProductForm.vue';
import { PRODUCTS } from '../mocks/data';

export default {
  name: 'ProductsList',
  components: { ProductForm, SearchProduct, Product },
  data: () => ({
    filterText: '',
    itemsPerPage: 10,
    sortedBy: undefined,
    currentPage: 1,
    products: PRODUCTS
  }),
  watch: {
    itemsPerPage() {
      this.currentPage = 1;
    }
  },
  computed: {
    filteredProducts() {
      let results = this.products;
      if (this.filterText) {
        results = this.products.filter((product) => product.name.toLowerCase().includes(this.filterText.toString().toLowerCase()));
      }
      return results.sort((product1, product2) => {
        if (this.sortedBy === 'A-Z') {
          return this.compareStrings(product1.name, product2.name);
        } else if (this.sortedBy === 'Created Date') {
          return product1.date - product2.date;
        }
      });
    },
    productsFromPage() {
      const start = (this.currentPage-1) * this.itemsPerPage;
      const end = start + this.itemsPerPage;
      return this.filteredProducts.slice(start, end);
    },
    totalPages() {
      return Math.ceil(this.filteredProducts.length / this.itemsPerPage);
    }
  },
  methods: {
    compareStrings(a, b) {
      if (a < b) {
        return -1;
      }
      if (a > b) {
        return 1;
      }
      return 0;
    }
  }
};
</script>

<style scoped>
.paginate-actions {
  margin-top: 20px;
}
.table-actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

strong {
  font-weight: bold;
}
</style>
