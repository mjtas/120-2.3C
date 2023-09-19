<template>
  <div>
    <h3>{{ book.title }}</h3>
    <p>Author: {{ book.author }}</p>
    <button @click="addToCart">Add to Cart</button>
  </div>
</template>

<script>
export default {
  props: {
    book: {
      type: Object, // The book object to display details
    },
    cart: {
    type: Array, // Pass the cart prop as an array
    required: true,
    },
  },
  
  methods: {
    addToCart() {
      if (this.book) {
        this.$emit('add-to-cart', this.book);
      }
    },
  },
}

</script>