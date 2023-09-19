<template>
  <div>
    <div v-if="book">
      <h2>{{ book.title }}</h2>
      <p>Author: {{ book.author }}</p>
      <p>Category: {{ book.category }}</p>
      <p v-if="book.available">Available</p>
      <p v-else>Not Available</p>
      <button @click="addToCart(book)">Add to Cart</button>
    </div>
    <div v-else>
      <p>Select a book to view details.</p>
    </div>
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
};
</script>