<template>
<div>
  <div class="image-section">
    <img :src="product.image" :alt="product.name">
    <div class="image-actions">
      <button class="btn-primary btn-small" type="submit">Replace</button>
      <button type="submit" class="btn-text btn-small">Clear</button>
    </div>
  </div>
  <text-field label="Image Title" />
  <text-field label="Alt Text" />
  <text-field label="Link" />
</div>
</template>

<script>
import TextField from './Utilities/TextField.vue';
export default {
  name: 'ProductForm',
  components: { TextField },
  props: {
    product: {
      type: Object,
      required: true
    }
  }
};
</script>

<style scoped>
img {
  width: 200px;
  height: 200px;
}
.image-section {
  display: flex;
  align-items: center;
  gap: 20px;
}
.image-actions {
  display: flex;
  flex-direction: column;
  gap: 8px;
}
</style>
