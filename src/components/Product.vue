<template>
  <div class="product">
    <div class="row">
      <div class="main-info">
        <img :src="product.image" alt="N/A">
        <em class="pointer mdi mdi-checkbox-blank-circle" :class="product.status"
           @click="toggleStatus"></em>
        <h5>{{ product.name }}</h5>
      </div>
      <div class="main-info">
        <p class="sm">{{ date }}</p>
        <button class="btn-fab" @click="expanded = !expanded">
          <em v-if="!expanded" class="mdi mdi-chevron-down"></em>
          <em v-else class="mdi mdi-chevron-up"></em>
        </button>
      </div>
    </div>
    <div v-show="expanded">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Product',
  props: {
    product: {
      type: Object,
      required: true
    }
  },
  data: () => ({
    expanded: false
  }),
  computed: {
    date() {
      if (this.product.date) {
        return new Date(this.product.date).toLocaleDateString();
      }
      return '';
    }
  },
  methods: {
    toggleStatus() {
      if (this.product.status === 'green') {
        this.product.status = 'yellow';
      } else if (this.product.status === 'yellow') {
        this.product.status = 'red';
      } else if (this.product.status === 'red') {
        this.product.status = 'green';
      }
    }
  }
};
</script>

<style scoped>
.product {
  border-bottom: 1px solid #F0F2F4;
}
.product .row {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}
.product img {
  width: 24px;
  height: 24px;
  border-radius: 2px;
}

.product .main-info {
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 12px;
}

.green {
  color: green;
}
.yellow {
  color: yellow;
}

.red {
  color: red;
}

.btn-fab {
  background-color: transparent;
  border: none;
  font-size: 24px;
  width: 24px;
  height: 24px;
  padding: 0;
  border-radius: 50%;
}

.btn-fab:hover {
  background-color: rgba(0,0,0,0.10);
  cursor: pointer;
}

.pointer {
  cursor: pointer;
}

@media screen and (max-width: 500px) {
  .sm {
    display: none;
  }
}

@media screen and (min-width: 500px) {
  .sm {
    display: initial;
  }
}
</style>
