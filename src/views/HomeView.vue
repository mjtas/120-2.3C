<template>
  <div class="home">
    <Library/>
  </div>
</template>

<script>
import Library from '@/components/Library.vue';
import BookDetails from '@/components/BookDetails.vue';
import BookItem from '@/components/BookItem.vue';

export default {
  name: 'HomeView',
  components: {
    Library,
    BookDetails,
    BookItem
  }
}
</script>
