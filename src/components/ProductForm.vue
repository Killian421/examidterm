<template>
  <form @submit.prevent="submitForm">
    <div>
      <label for="productName">Product Name:</label>
      <input type="text" v-model="product.name" required />
    </div>
    <div>
      <label for="productPrice">Price:</label>
      <input type="number" v-model="product.price" required />
    </div>
    <div>
      <label for="productDescription">Description:</label>
      <textarea v-model="product.description" required></textarea>
    </div>
    <button type="submit">Add Product</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      product: {
        name: '',
        price: '',
        description: '',
      },
    }
  },
  methods: {
    submitForm() {
      this.$emit('add-product', { ...this.product })
      this.product.name = ''
      this.product.price = ''
      this.product.description = ''
    },
  },
}
</script>

<style scoped>
/* Add your styles here */
</style>
