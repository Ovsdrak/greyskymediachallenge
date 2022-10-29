<template>
  <div class="form-group">
    <label>{{ label }}</label>
    <input class="text-field"
           :value="$attrs.value"
           :placeholder="label"
           @input="$emit('input', $event)"
           type="text" placeholder="Find a Product">
  </div>
</template>

<script>
export default {
  name: 'TextField',
  props: {
    label: {
      required: true,
      type: String
    }
  }
};
</script>

<style scoped>
label {
  font-weight: bold;
  color: #585656;
}
.form-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin: 8px 0;
}
</style>
