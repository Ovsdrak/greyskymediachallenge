<template>
  <form class="wrapper" @submit.prevent="onSearch">
    <input class="text-field" v-model="searchText" type="text" placeholder="Find a Product">
    <button class="btn-primary" type="submit">Search</button>
  </form>
</template>

<script>
export default {
  name: 'SearchProduct',
  data: () => ({
    searchText: ''
  }),
  methods: {
    onSearch() {
      this.$emit('change', this.searchText);
    }
  }
};
</script>

<style scoped>
.wrapper {
  display: flex;
  gap: 8px;
}

</style>
