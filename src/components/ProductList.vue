<template>
  <div>
    <h2>Product List</h2>
    <ul>
      <li v-for="(product, index) in products" :key="index">
        <div>
          <h3>{{ product.name }}</h3>
          <p>Price: ${{ product.price }}</p>
          <p>Description: {{ product.description }}</p>
          <button @click="editProduct(index)">Edit</button>
        </div>
      </li>
    </ul>
    <ProductForm
      v-if="isEditing"
      @add-product="updateProduct"
      :product="currentProduct"
    />
  </div>
</template>

<script>
import ProductForm from './ProductForm.vue'

export default {
  components: {
    ProductForm,
  },
  props: {
    products: Array,
  },
  data() {
    return {
      isEditing: false,
      currentProduct: null,
      currentIndex: null,
    }
  },
  methods: {
    editProduct(index) {
      this.isEditing = true
      this.currentIndex = index
      this.currentProduct = { ...this.products[index] }
    },
    updateProduct(updatedProduct) {
      this.$emit('update-product', {
        index: this.currentIndex,
        product: updatedProduct,
      })
      this.isEditing = false
      this.currentProduct = null
      this.currentIndex = null
    },
  },
}
</script>

<style scoped>
/* Add your styles here */
</style>
